+++
date = 2026-02-09
title = "Chapter 02: Installing Rust on Windows (using WSL/Ubuntu)"
description = "For young learners! Learn how to install Rust on your Windows computer by first setting up Ubuntu using Windows Subsystem for Linux (WSL), then installing Rust within that Linux environment."
[taxonomies]
tags = ["rust", "installation", "tutorial", "cli", "education", "kids", "children", "young", "learners", "ttk", "windows", "wsl", "ubuntu"]
+++

Hello, Windows Adventurer!

If you're using a computer with Windows, this chapter is for you! We're going to
install Rust inside your **Ubuntu Linux** system that you set up using **WSL
(Windows Subsystem for Linux)**. This is the best way to code with Rust on
Windows!

## Prerequisite: Install Ubuntu with WSL first

Before you can install Rust with these instructions, you need to have **Ubuntu
Linux** set up on your Windows computer using WSL. If you haven't done that yet,
please go to this course first:

- [Install Ubuntu with WSL: Your Linux Adventure on Windows!](@/ttk/install-wsl/_index.md)

Once you have Ubuntu running with WSL, come back here!

## Step 1: Open Your Ubuntu Terminal

First, open your **Ubuntu terminal**. You can do this by searching for "Ubuntu"
in your Windows Start menu and clicking the app. It's the black window where you
type Linux commands!

## Step 2: Update Your Ubuntu System (Important First Step!)

Before installing anything new, it's always a good idea to update all the
software on your Ubuntu system. This ensures everything is fresh and ready!

In your Ubuntu terminal, type this, then press Enter:

```bash
sudo apt update
sudo apt upgrade -y
```

Type your Linux password if it asks, and press Enter. This command tells Ubuntu
to get the newest lists of apps and then install new versions of apps.

## Step 3: Install Rustup

Rustup is the easiest way to install Rust. It's a special tool that helps manage
different versions of Rust.

In your Ubuntu terminal, type this command and press Enter:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

You'll see some messages. When it asks:

`1) Proceed with installation (default)`

Just press **Enter** to choose the default option. This will download and
install Rust!

## Step 4: Restart Your Ubuntu Terminal

After Rust is installed, it's a good idea to close your Ubuntu terminal window
and open a new one. This helps your Ubuntu system "refresh" and find the new
Rust tools.

## Step 5: Verify Your Installation

Let's check if Rust and Cargo (Rust's build tool) are installed correctly!

In your **new** Ubuntu terminal window, type these commands, one by one, and
press Enter after each:

```bash
rustc --version
cargo --version
```

You should see something like: `rustc 1.XX.X (YYYY-MM-DD)`
`cargo 1.XX.X (YYYY-MM-DD)`

The `1.XX.X` part will be the version number, which might be different from this
example, and that's perfectly fine! As long as you see version numbers, Rust is
installed!

Congratulations! Rust is now installed on your Windows computer, inside your
Ubuntu Linux system. You're ready to start coding your Quest App!

## Navigation

- Previous:
  [Chapter 01: Installing Rust on Linux (Arch)](@/ttk/install-rust/01-linux-arch.md)
- Next: [Chapter 03: Installing Rust on macOS](@/ttk/install-rust/03-macos.md)
