+++
date = 2026-01-31
title = "A Deep-Dive Tutorial: Building a Universal Autofill System with Rofi, Pass, and Wtype"
description = "A step-by-step guide to creating a universal, keyboard-driven autofill system for any application on Linux using pass, rofi, and wtype, based on my personal dotfiles setup."
[taxonomies]
tags = ["linux", "dotfiles", "password-management", "pass", "rofi", "wtype", "hyprland", "automation", "security", "tutorial"]
+++

In a previous article, I introduced my
[seamless password management setup](@/blog/2026-01-28-seamless-password-management-on-linux.md).
It's one of the most powerful and unique parts of my dotfiles, providing a
universal, keyboard-driven autofill system that works on any application. Today,
we're going to build it from the ground up.

This tutorial will walk you through creating the scripts and configuration
needed to replicate this system, using your `pass` password store, `rofi` for an
interactive menu, and `wtype` to simulate keyboard input.

## The Goal: Frictionless & Universal Autofill

The goal is simple: press a hotkey, get a fuzzy-searchable list of your
passwords, select one, and have it automatically typed into whatever application
is currently active—be it a browser, a terminal, or a native GUI application.

## Prerequisites

Before we start, you'll need a few tools. This guide is based on my setup, which
uses a Wayland compositor (Hyprland), but I'll provide notes for X11 users where
applicable.

- **`pass`:**
  [The standard Unix password manager](https://www.passwordstore.org/). Your
  password store should be initialized and populated.
- **`pass-otp`:** The
  [pass extension for TOTP](https://github.com/tadfisher/pass-otp).
- **`rofi`:** A versatile window switcher and application launcher. We'll use it
  as a dynamic menu.
- **`wtype`:** A Wayland tool to simulate keyboard input. For X11 users,
  **`xdotool`** is the equivalent.
- **`jq`:** A command-line JSON processor, used to parse window information.
- **(Optional but recommended) `hyprctl`:** The command-line utility for
  Hyprland, used to get the active window title. X11 users can use `xdotool`.

## Step 1: The Core Script (`.menu-pass`)

This is the engine of our autofill system. It's responsible for displaying the
menu, retrieving the selected credential from `pass`, and "typing" it into the
active window.

Create a script named `.menu-pass` in your local bin directory (e.g.,
`~/.local/bin/.menu-pass`) and make it executable
(`chmod +x ~/.local/bin/.menu-pass`).

```bash
#!/usr/bin/env bash

# A script to provide a rofi-based pass-menu, with automatic typing.
# Dependencies: pass, pass-otp, rofi, wtype (for Wayland) or xdotool (for X11)

# --- Configuration ---
# Use wtype for Wayland, xdotool for X11
# Wayland
WTYPE_CMD="wtype"
# X11
# XDO_CMD="xdotool type --clearmodifiers"

# --- Script Logic ---
shopt -s nullglob globstar

# Get the directory of the password store
PASSWORD_STORE_DIR=${PASSWORD_STORE_DIR-~/.password-store}
cd "$PASSWORD_STORE_DIR" || exit 1

# Get all password files
password_files=(**/*.gpg)
passwords=("${password_files[@]%.gpg}")

# Determine the mode from the first argument (auth, user, pass, otp)
MODE=${1:-pass} # Default to 'pass' mode if no argument is given
shift

# If there's a second argument, use it to filter the password list
if [ -n "$1" ]; then
    passwords=($(printf "%s\n" "${passwords[@]}" | grep -i "$1"))
fi

# Present the password list to rofi for selection
selection=$(printf "%s\n" "${passwords[@]}" | rofi -dmenu -p "Pass [${MODE}]" -i)
[[ -z "$selection" ]] && exit 1

# --- Handle Selection Based on Mode ---
case "$MODE" in
    "auth")
        user=$(basename "$selection")
        pass=$(pass show "$selection" | head -n 1)
        # Type username, Tab, then password
        $WTYPE_CMD "$user"
        $WTYPE_CMD -k tab
        $WTYPE_CMD "$pass"
        $WTYPE_CMD -k return
        ;;
    "user")
        token=$(basename "$selection")
        $WTYPE_CMD "$token"
        $WTYPE_CMD -k return
        ;;
    "pass")
        token=$(pass show "$selection" | head -n 1)
        $WTYPE_CMD "$token"
        $WTYPE_CMD -k return
        ;;
    "otp")
        token=$(pass otp "$selection")
        $WTYPE_CMD "$token"
        $WTYPE_CMD -k return
        ;;
    *)
        echo "Invalid mode: $MODE" >&2
        exit 1
        ;;
esac

exit 0
```

### How It Works

1. **Configuration:** It sets the command for typing. If you're on X11, you
   would comment out `WTYPE_CMD` and uncomment `XDO_CMD`.
2. **Password Discovery:** It finds all your encrypted password files (`.gpg`)
   within your password store.
3. **Mode Handling:** It checks the first argument (`$1`) to determine what you
   want to do:
   - `auth`: Type username, a Tab, and then the password (great for web logins).
   - `user`: Type only the username.
   - `pass`: Type only the password.
   - `otp`: Generate and type a one-time password.
4. **Filtering:** If a second argument is provided, it filters the password list
   using `grep`. This is key for our context-aware functionality.
5. **Rofi Menu:** It pipes the list of passwords into `rofi -dmenu`, which
   displays an interactive, searchable menu.
6. **Typing:** Based on the selected mode, it retrieves the appropriate
   information using `pass` and then uses `wtype` to simulate key presses for
   the active window.

## Step 2: The Context-Aware Wrapper (`.menu-autofill`)

This script is the "smart" layer. It figures out what application you're using
and provides a relevant filter to `.menu-pass`. This is what makes the system
feel so magical.

Create a script named `.menu-autofill` in the same directory
(`~/.local/bin/.menu-autofill`) and make it executable.

```bash
#!/usr/bin/env bash

# A wrapper script that determines the active window and calls .menu-pass with a filter.
# This version is for Hyprland (Wayland).

# --- Script Logic ---
# Get the title of the active window using hyprctl and parse it with jq
TITLE=$(hyprctl activewindow -j | jq -r '.title')

# Determine the mode from the first argument (e.g., 'auth', 'pass')
MODE=${1:-pass} # Default to 'pass'

# Extract a domain-like string from the window title to use as a filter
# This regex looks for patterns like 'sub.domain.com'
DOMAIN=$(echo "$TITLE" | grep -oP '(?<=[-—_.\s\[\(])\b[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}\b' | head -n 1)

# Call the core script with the determined mode and the domain filter
# The trailing '/' helps match directory-based password entries in 'pass'
~/.local/bin/.menu-pass "$MODE" "$DOMAIN"
```

### How It Works

1. **Get Active Window Title:** It uses `hyprctl activewindow -j` to get a JSON
   output describing the active window and `jq` to parse out the `.title` field.
   (For X11, you could use something like
   `xdotool getactivewindow getwindowname`).
2. **Extract Domain:** It uses a regular expression to find a domain name within
   the window title. This is surprisingly effective for web browsers, SSH
   sessions, and many other applications.
3. **Call `.menu-pass`:** It executes our core script, passing the desired
   `MODE` (defaulting to `pass`) and the extracted `DOMAIN` as a filter.

## Step 3: Tying It All Together with a Hotkey

The final step is to bind our `.menu-autofill` script to a keyboard shortcut in
your window manager's configuration. Here's how I do it in my
`~/.config/hypr/hyprland.conf`:

```ini
# ~/.config/hypr/hyprland.conf

# ... other binds ...

# Password Management / Autofill
bind = $mod ctrl, j,         exec, ~/.local/bin/.menu-autofill auth
bind = $mod ctrl, k,         exec, ~/.local/bin/.menu-autofill user
bind = $mod ctrl, l,         exec, ~/.local/bin/.menu-autofill pass
bind = $mod ctrl, semicolon, exec, ~/.local/bin/.menu-autofill otp
```

With these bindings:

- `Super + Ctrl + J` will show a filtered list and type `username`, `Tab`, then
  `password` (for authentication).
- `Super + Ctrl + K` will show a filtered list and type only the `username`.
- `Super + Ctrl + L` will show a filtered list and type only the `password`.
- `Super + Ctrl + Semicolon` will show a filtered list and type the selected
  One-Time Password (OTP).

## Conclusion

You now have a complete, universal autofill system that is secure, incredibly
efficient, and works across your entire Linux desktop. It's a perfect example of
the power of composing simple, effective CLI tools to create a workflow that is
tailored precisely to your needs.

This system is fully customizable. You can tweak the regular expression in
`.menu-autofill`, change the `rofi` theme, or add new modes to `.menu-pass`. I
encourage you to take this foundation and adapt it to make it truly your own.
Happy hacking!
