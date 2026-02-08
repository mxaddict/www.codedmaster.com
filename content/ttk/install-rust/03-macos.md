+++
date = 2026-02-09
title = "Chapter 03: Installing Rust on macOS"
description = "For young learners! Learn how to install Rust on your macOS computer using the terminal, step-by-step."
[taxonomies]
tags = ["rust", "installation", "tutorial", "cli", "education", "kids", "children", "young", "learners", "ttk", "macos", "homebrew", "xcode"]
+++

Hello, macOS Adventurer!

If you're using a computer with macOS, this chapter is for you! We'll use a special script to install Rust, which makes things very easy.

### Step 1: Install Xcode Command Line Tools (If You Haven't Already)

Rust needs some special tools from Apple called "Xcode Command Line Tools" to build programs. You might already have them! If not, don't worry, it's easy to get.

Open your **Terminal** (you can find it in Applications > Utilities, or by searching with Spotlight).

Type this command and press Enter:

```bash
xcode-select --install
```

If the tools are not installed, a window will pop up asking you to install them. Click "Install" and agree to the terms. This might take a little while. If you already have them, you'll see a message saying something like "xcode-select: error: command line tools are already installed". That's great!

### Step 2: Install Homebrew (Optional, but Recommended for Mac Users!)

Homebrew is a "package manager" for macOS. Think of it like a super-smart app store for your Terminal that helps you install other tools easily. Many developers use it! If you already have Homebrew, you can skip this step.

To install Homebrew, copy and paste this command into your Terminal and press Enter:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the instructions in the Terminal. It might ask for your computer's password. Press Enter when it asks you to.

After it's done, it might tell you to run a couple of commands to add Homebrew to your "PATH" (where your computer looks for programs). Make sure to run those commands!

### Step 3: Install Rustup

Rustup is the easiest way to install Rust. It's a special tool that helps manage different versions of Rust.

In your Terminal, copy and paste this command and press Enter:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

You'll see some messages. When it asks:

`1) Proceed with installation (default)`

Just press **Enter** to choose the default option. This will download and install Rust!

After installation, it might tell you to "source" your `~/.profile` or `~/.bashrc` or `~/.zshrc` file. This means reloading your Terminal's settings. The easiest way to do this is to simply **close your Terminal window and open a new one.**

### Step 4: Verify Your Installation

Let's check if Rust and Cargo (Rust's build tool) are installed correctly!

In your **new** Terminal window, type these commands, one by one, and press Enter after each:

```bash
rustc --version
cargo --version
```

You should see something like:
`rustc 1.XX.X (YYYY-MM-DD)`
`cargo 1.XX.X (YYYY-MM-DD)`

The `1.XX.X` part will be the version number, which might be different from this example, and that's perfectly fine! As long as you see version numbers, Rust is installed!

Congratulations! Rust is now installed on your macOS computer. You're ready to start coding your Quest App!

## Navigation
- Previous: [Chapter 02: Installing Rust on Windows](@/ttk/install-rust/02-windows.md)
