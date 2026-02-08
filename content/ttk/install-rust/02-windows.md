+++
date = 2026-02-09
title = "Chapter 02: Installing Rust on Windows"
description = "For young learners! Learn how to install Rust on your Windows computer, step-by-step, including setting up development tools."
[taxonomies]
tags = ["rust", "installation", "tutorial", "cli", "education", "kids", "children", "young", "learners", "ttk", "windows"]
+++

Hello, Windows Adventurer!

If you're using a computer with Windows, this chapter is for you! Installing
Rust on Windows is a bit like setting up a new game – you download an installer
and follow the instructions.

### Step 1: Download the Rust Installer

Open your favorite web browser (like Chrome, Edge, or Firefox) and go to the
official Rust website:

[**https://www.rust-lang.org/tools/install**](https://www.rust-lang.org/tools/install)

Look for the big button that says **"Download rustup-init.exe"** (or something
similar). Click it to download the installer file.

### Step 2: Run the Installer

Once the file `rustup-init.exe` has finished downloading, find it (usually in
your "Downloads" folder) and double-click it to run it.

A special black window (the Command Prompt) will open. It will ask you some
questions.

You'll usually see an option like this:

`1) Proceed with installation (default)`

Just press **Enter** to choose the default option, which will install everything
you need!

The installer will then download and install Rust and its tools. This might take
a few minutes, depending on your internet speed.

### Step 3: Install Build Tools (Important!)

Rust needs some extra "build tools" from Microsoft to work correctly on Windows.
The installer will usually prompt you to install these.

If you see a message like:

`The Visual Studio build tools haven't been detected.`
`Would you like to install them? (Y/n)`

Type **`Y`** and press **Enter**. This will open another window from Microsoft
to install "Visual Studio Build Tools". Follow the instructions there to install
the necessary components. You usually just need to select the "Desktop
development with C++" workload if prompted, or just click "Install" if it's
simplified.

This step is very important, so make sure it finishes correctly!

### Step 4: Restart Your Terminal

After Rust and the build tools are installed, close the Command Prompt window
you used for installation. You might even need to restart your computer for
everything to work perfectly.

Then, open a **new** Command Prompt or PowerShell window. This helps your
computer "refresh" and find the new Rust tools.

### Step 5: Verify Your Installation

Let's check if Rust and Cargo (Rust's build tool) are installed correctly!

In your **new** Command Prompt or PowerShell window, type these commands, one by
one, and press Enter after each:

```bash
rustc --version
cargo --version
```

You should see something like: `rustc 1.XX.X (YYYY-MM-DD)`
`cargo 1.XX.X (YYYY-MM-DD)`

The `1.XX.X` part will be the version number, which might be different from this
example, and that's perfectly fine! As long as you see version numbers, Rust is
installed!

Congratulations! Rust is now installed on your Windows computer. You're ready to
start coding your Quest App!

## Navigation

- Previous:
  [Chapter 01: Installing Rust on Linux (Arch)](@/ttk/install-rust/01-linux-arch.md)
- Next: [Chapter 03: Installing Rust on macOS](@/ttk/install-rust/03-macos.md)
