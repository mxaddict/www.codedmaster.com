+++
date = 2026-02-09
title = "Chapter 02: Setting Up Ubuntu in WSL"
description = "For young learners! Learn how to set up your Ubuntu Linux environment within WSL, including creating a username and password."
[taxonomies]
tags = ["wsl", "windows", "linux", "ubuntu", "installation", "tutorial", "education", "kids", "children", "young", "learners", "ttk", "ubuntu", "setup", "terminal"]
+++

Hello, Ubuntu Explorer!

Now that WSL is installed on your Windows computer, it's time to set up your
very own Ubuntu Linux system!

## Step 1: Launch Ubuntu for the First Time

If you just finished the previous chapter and restarted your computer, Ubuntu
might have automatically started for the first time. If not, don't worry!

To open your new Ubuntu Linux terminal:

1. Click on the **Windows Start button**.
2. Type "Ubuntu".
3. Click on the "Ubuntu" app that appears (it might say "Ubuntu 22.04 LTS" or a
   different version number).

A brand new black window will open. This is your Ubuntu Linux terminal!

## Step 2: Create Your Linux Username and Password

The first time Ubuntu runs, it will ask you to create a username and password
for your new Linux system. This is important for security, just like your
Windows password.

- **For username:** Type a username you like (it can be your first name, or a
  fun code name!). Press Enter.
- **For password:** Type a password. **You won't see anything appear as you
  type**, and that's normal for security. Just type it carefully and press
  Enter.
- **Retype password:** Type the same password again to make sure you didn't make
  a mistake. Press Enter.

Remember this username and password! You'll need it whenever you install new
software or make important changes in your Ubuntu terminal.

## Step 3: Update Ubuntu's Software List

Just like we update Windows, it's a good idea to update Ubuntu! This makes sure
all the lists of available software are fresh and new.

In your Ubuntu terminal, type these commands, pressing Enter after each:

```bash
sudo apt update
sudo apt upgrade -y
```

- `sudo apt update`: This command asks Ubuntu to get the newest lists of
  software from the internet.
- `sudo apt upgrade -y`: This command tells Ubuntu to install any new versions
  of software that are already on your system. The `-y` means "yes" to all
  questions, so you don't have to keep typing `Y`.

This process might take a few minutes. If it asks for your password, type the
Linux password you just created.

## Step 4: You're Ready to Go

Once the update is finished, you have a fully working Ubuntu Linux system right
inside your Windows! You can now use this terminal to install Linux software,
run commands, and begin your coding adventures.

To close the Ubuntu terminal, you can just type `exit` and press Enter, or click
the 'X' button on the window. To open it again, just find the Ubuntu app in your
Start menu!

Congratulations! You've set up Ubuntu Linux with WSL. Now you're ready to
install Rust and Vim inside your new Linux environment!

## Navigation

- Previous:
  [Chapter 01: Getting Started with WSL](@/ttk/install-wsl/01-wsl-setup.md)
