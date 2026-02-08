+++
date = 2026-02-09
title = "Chapter 01: Installing Rust on Linux (Arch)"
description = "For young learners! Learn how to install Rust on your Arch Linux computer using the terminal, step-by-step."
[taxonomies]
tags = ["rust", "installation", "tutorial", "cli", "education", "kids", "children", "young", "learners", "ttk", "linux", "arch linux", "pacman"]
+++

Hello, Linux Adventurer!

If you're using a computer with Arch Linux, this chapter is for you! We'll use
the `pacman` command, which is like your computer's app store, to install Rust.

## Step 1: Update Your System (Important First Step!)

Before installing anything new, it's always a good idea to update all the
software on your computer. This ensures everything is fresh and ready!

Open your **terminal** (the black screen where you type commands) and type this,
then press Enter:

```bash
sudo pacman -Syu
```

Type your computer's password if it asks, and press Enter. This command tells
`pacman` to "synchronize" (get new lists of apps) and "update" (install new
versions of apps).

## Step 2: Install Rustup

Rustup is the easiest way to install Rust. It's a special tool that helps manage
different versions of Rust.

In your terminal, type this command and press Enter:

```bash
sudo pacman -S rustup
```

When it asks `(Y/n)`, type `Y` and press Enter to say "Yes, install it!"

## Step 3: Install the Rust Toolchain

Now that `rustup` is installed, we can use it to get the main Rust tools. We'll
install the "stable" version, which is the most reliable one.

Type this command and press Enter:

```bash
rustup default stable
```

You might see some messages pop up. This is Rustup doing its work!

## Step 4: Update Rust (Good Practice!)

It's a good habit to keep your Rust tools updated.

Type this command and press Enter:

```bash
rustup update
```

This will check if there are any newer versions of Rust and install them if
needed.

## Step 5: Verify Your Installation

Let's check if Rust and Cargo (Rust's build tool) are installed correctly!

Type these commands, one by one, and press Enter after each:

```bash
rustc --version
cargo --version
```

You should see something like: `rustc 1.XX.X (YYYY-MM-DD)`
`cargo 1.XX.X (YYYY-MM-DD)`

The `1.XX.X` part will be the version number, which might be different from this
example, and that's perfectly fine! As long as you see version numbers, Rust is
installed!

Congratulations! Rust is now installed on your Arch Linux computer. You're ready
to start coding your Quest App!

## Navigation

- Previous: [Install Rust: Get Ready to Code!](@/ttk/install-rust/_index.md)
- Next:
  [Chapter 02: Installing Rust on Windows](@/ttk/install-rust/02-windows.md)
