+++
date = 2026-01-28
title = "Seamless Password Management: Integrating pass, pass-otp, and Dynamic Autofill on Linux"
description = "Discover a powerful dotfiles setup for secure and efficient password management and autofill on any Linux application, leveraging pass, pass-otp, rofi, and wtype."
[taxonomies]
tags = ["linux", "dotfiles", "password management", "pass", "security", "autofill", "rofi", "wtype", "hyprland"]
+++

In today's digital landscape, robust password management is non-negotiable.
While many solutions exist, they often come with tradeoffs between security,
convenience, and platform compatibility. For Linux users, especially those who
prefer a keyboard-driven workflow, traditional browser extensions or standalone
password managers might feel clunky or restrictive.

This article dives into a custom dotfiles solution that leverages the power of
`pass` (the Unix password manager), `pass-otp` for two-factor authentication,
and a pair of clever scripts—`.menu-pass` and `.menu-autofill`—to provide
dynamic autofill capabilities for _any_ application on your Linux machine.

## The Core: `pass` and `pass-otp`

At the heart of this system is `pass`, a simple yet incredibly powerful password
manager. `pass` stores each password in a GPG-encrypted file, typically within a
git repository. This approach offers several compelling benefits:

- **Simplicity:** Passwords are plain text files, easily viewable once
  decrypted.
- **Security:** GPG encryption ensures your secrets are protected at rest.
- **Version Control:** Storing your password store in Git means you have a full
  history of changes, easy synchronization across devices, and robust backups.
- **Extensibility:** `pass` has a rich ecosystem of extensions, including
  `pass-otp`, which generates time-based one-time passwords (TOTP) directly from
  your password store, eliminating the need for a separate authenticator app.

## Interactive Selection with `.menu-pass`

The `.menu-pass` script acts as the intelligent interface between your desire
for a password and the `pass` utility. It provides an interactive menu and
handles the "typing" of credentials into your active application.

Here's a breakdown of its functionality:

- **Versatile Modes:** `.menu-pass` supports multiple modes, specified as an
  argument:
  - `auth`: Ideal for login forms. It types the username, presses `Tab`, types
    the password, and then presses `Return`.
  - `user`: Types only the username associated with a password entry.
  - `pass`: Types only the password (the first line of the `pass` entry).
  - `otp`: Generates and types a one-time password using `pass otp`.
- **`rofi` for Selection:** The script uses `rofi -dmenu` to present an
  interactive, searchable menu of your `pass` entries. This allows for quick
  filtering and selection of the correct credential, even if you have hundreds
  of entries.
- **`wtype` for Input Simulation:** The magic ingredient that makes this system
  universal is `wtype`. This utility simulates keyboard input directly into the
  active window. This means whether you're in a web browser, a terminal, or a
  desktop application, `.menu-pass` can "type" your sensitive information
  without needing application-specific integrations.

```bash
#!/usr/bin/env bash

# ... (variable definitions and mode checks) ...

selection=$(echo "$entries" | rofi -dmenu -p "[$MODE]" -i)
[[ -z "$selection" ]] && exit 1

if [[ "$MODE" == "auth" ]]; then
    user=$(basename "$selection")
    pass=$(pass show "$selection" | head -n 1)
    # Using wtype to simulate key presses
    $WTYPE "$user"
    $WTYPE -k Tab
    $WTYPE "$pass"
    $WTYPE -k Return
    exit 0
elif [[ "$MODE" == "user" ]]; then
    token=$(basename "$selection")
elif [[ "$MODE" == "pass" ]]; then
    token=$(pass show "$selection" | head -n 1)
elif [[ "$MODE" == "otp" ]]; then
    token=$(pass otp "$selection")
fi

$WTYPE "$token"
$WTYPE -k Return
```

## Dynamic Context with `.menu-autofill`

While `.menu-pass` handles the retrieval and typing, `.menu-autofill` provides
the context. Its primary job is to intelligently determine what password entry
you likely need based on your active application.

- **Active Window Inspection:** This script is designed for Wayland
  environments, specifically leveraging `hyprctl` (from Hyprland) and `jq` to
  fetch the title of the currently focused window.
- **Domain Extraction:** From the window title, it uses a regular expression to
  extract a domain name. For example, if your browser title is "Sign in -
  GitHub", it will attempt to extract "github.com". This domain is then used to
  pre-filter the `pass` entries, significantly speeding up your selection.
- **Delegation:** Finally, `.menu-autofill` calls `.menu-pass`, passing along
  the determined mode (e.g., `pass`, `auth`) and the extracted domain as a
  filter.

```bash
#!/usr/bin/env bash

TITLE=$(hyprctl activewindow -j | jq -r '.title')

MODE=${1:-pass} # Default to 'pass' mode if not specified
DOMAIN=$(echo "$TITLE" | grep -oP '(?<=//)[a-z0-9.-]+\.[a-z]{2,}' | head -n 1)

# Calls .menu-pass with the inferred domain
.menu-pass "$MODE" "$DOMAIN/"
```

## Putting It All Together: The Workflow

Imagine you're browsing the web and land on a login page. Here's how this
integrated system streamlines your workflow:

1. **Hotkey Activation:** You press a predefined hotkey (e.g., `Super + P`).
   This hotkey is configured in your window manager (like Hyprland) to execute
   `.menu-autofill`.
2. **Contextual Awareness:** `.menu-autofill` quickly queries your active
   window, extracts the relevant domain (e.g., `example.com`), and passes this
   to `.menu-pass`.
3. **Filtered Selection:** `.menu-pass` launches `rofi`, presenting you with a
   list of `pass` entries already filtered to `example.com`.
4. **Credential Input:** You select the desired entry, and `.menu-pass` uses
   `wtype` to flawlessly type your username, password, or OTP directly into the
   active input fields.

This entire process takes mere seconds, providing a frictionless and secure
login experience across all your applications.

## Benefits of This Approach

- **Enhanced Security:** Your passwords remain GPG-encrypted. There's no
  reliance on browser-specific password managers that can be vulnerable to
  certain attacks.
- **Universal Compatibility:** Because it uses `wtype` to simulate keyboard
  input, this solution works with virtually any application that accepts text
  input, from web browsers to command-line interfaces to native desktop apps.
- **Total Control & Customization:** As these are simple shell scripts in your
  dotfiles, you have complete control to modify, extend, or adapt them to your
  specific needs and preferences.
- **Efficiency:** The combination of `rofi`'s fast selection and `wtype`'s rapid
  input makes password entry incredibly quick.
- **Privacy:** All operations occur locally on your machine; no third-party
  services are involved in the autofill process.

## Customization and Further Improvements

- **X11 Support:** For X11 users, `xdotool` can replace `wtype` for input
  simulation and `xdotool getactivewindow getwindowname` can replace `hyprctl`
  for window title retrieval.
- **Alternative Fuzzy Finders:** While `rofi` is excellent, you could substitute
  it with `fzf`, `dmenu`, or any other interactive selection tool.
- **More Advanced Logic:** Extend `.menu-autofill` to handle different window
  title patterns or integrate with other context-aware tools.

## Conclusion

By combining the simplicity and security of `pass` with the scripting power of
the Linux ecosystem, these dotfiles provide a sophisticated yet highly adaptable
password management solution. It's a testament to the flexibility of Linux that
such a seamless, secure, and universal autofill experience can be crafted with
just a few lines of shell script. Embrace the power of your dotfiles and elevate
your password game!
