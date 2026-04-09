+++
date = 2026-02-09
title = "Supercharging Your Dotfiles: QOL Improvements, Fedora Support, and Cleaner Updates"
description = "Discover how recent enhancements to my dotfiles, including silent output, detailed logging, and expanded Fedora Linux support, streamline development workflows and system maintenance for a more efficient command-line experience."
[taxonomies]
tags = ["automation", "bash", "customization", "devops", "dotfiles", "fedora", "linux", "scripting", "system", "tools"]
+++

## Introduction

This article details the recent updates and modifications to my personal
dotfiles, with a particular focus on the `~/.local/bin/.update` and
`~/.local/bin/.deps` scripts. These changes aim to streamline my development
workflow, enhance system maintenance, and improve overall efficiency.

## The `.update` Script

The `.update` script is designed to automate the process of updating various
components of my system. It now includes enhanced functionalities for:

- **System package management:** (e.g., `paru -Syu` on Arch Linux,
  `apt update && apt upgrade` on Debian/Ubuntu).
- **Dotfile synchronization:** Pulling the latest changes from my dotfiles
  repository.
- **Application-specific updates:** (e.g., `nvim` plugin updates, `tldr` cache
  updates, `tmux` plugin updates).

### Quality of Life Improvements in `.update`

Significant quality of life improvements have been integrated into the `.update`
script to enhance its user experience and reliability:

- **Robust Error Handling:** The script now utilizes `set -euo pipefail` to
  ensure immediate exits on errors, unset variables, or failed commands within a
  pipeline. This drastically improves the script's reliability and prevents
  unexpected behavior.
- **Silent Execution:** Most commands executed by the script now pipe their
  output to `>/dev/null 2>&1`. This keeps the terminal clean and focused,
  preventing a flood of command-line output and allowing the user to concentrate
  on essential updates.
- **Clear, Step-by-Step Logging:** Instead of raw command output, the script
  provides concise and visually appealing feedback using
  `echo -e "$GREEN_CHECK ..."`. Each major step of the update process is clearly
  indicated with a green checkmark, making it easy to track progress and
  identify the current operation at a glance.
- **Automated Dotfiles Stashing and Reapplication:** Before pulling updates, the
  script now intelligently stashes any local, uncommitted changes to the
  dotfiles repository. After a successful pull, these changes are automatically
  reapplied, ensuring that personal modifications are preserved across updates.
- **Self-Correction for Updates:** If the dotfiles repository itself updates the
  `.update` script, the script is designed to re-execute itself with the new
  version, ensuring that the latest logic and features are always in use.

## The `.deps` Script

The `.deps` script is responsible for managing and installing project
dependencies across different operating systems. Recent changes have focused on:

- **Cross-platform compatibility:** Ensuring dependencies can be easily set up
  on different operating systems (e.g., Linux distributions like Arch, Fedora,
  Debian/Ubuntu, as well as macOS/Homebrew), including essential tools and
  libraries.

### Enhanced Cross-Platform Dependency Management with Fedora Support

The `.deps` script has been significantly enhanced to provide robust
cross-platform dependency management. A key addition is the explicit support for
**Fedora**, which is now detected via the `dnf` package manager. This means
users on Fedora can now seamlessly install core system packages with a simple
execution of the `.deps` script.

Similar to the `.update` script, `.deps` also benefits from:

- **Robust Error Handling:** Employing `set -euo pipefail` for safer and more
  predictable execution.
- **Silent Execution:** Most package installation commands are run with output
  redirection (`>/dev/null 2>&1`) to maintain a clean and uncluttered terminal.
- **Clear, Step-by-Step Logging:** Progress is communicated through clear
  `echo -e "$GREEN_CHECK ..."` messages, making it easy to understand which
  dependencies are being addressed for a particular operating system.

The script intelligently identifies the operating system's package manager
(e.g., `pacman` for Arch, `dnf` for Fedora, `apt-get` for Debian/Ubuntu, `brew`
for macOS) and executes the appropriate installation commands. This ensures that
the correct development environment is set up with minimal manual intervention.

## Future Plans

I plan on updating my **hyprland**, **waybar**, **swaync**, **gnome**, **qt**,
etc. configurations to use **matugen** for the color scheme and base the colors
on the currently set wallpaper in **hyprpaper**. This will be major change to my
current dotfiles theme setup which is completely static and set to a
**tokyonight** inspired color palette

## Conclusion

These updates to my dotfiles, particularly the `.update` and `.deps` scripts,
represent a significant step towards a more automated, efficient, and robust
development environment.
