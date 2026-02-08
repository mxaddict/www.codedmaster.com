+++
date = 2026-02-09
title = "Chapter 02: Installing Vim on Windows (using WSL/Ubuntu)"
description = "For young learners! Learn how to install Vim on your Windows computer by first setting up Ubuntu using Windows Subsystem for Linux (WSL), then installing Vim within that Linux environment."
[taxonomies]
tags = ["vim", "editor", "cli", "installation", "tutorial", "education", "kids", "children", "young", "learners", "ttk", "windows", "wsl", "ubuntu"]
+++

Hello, Windows Adventurer!

If you're using a computer with Windows, this chapter is for you! We're going to
install Vim inside your **Ubuntu Linux** system that you set up using **WSL
(Windows Subsystem for Linux)**. This is the best way to use Vim on Windows!

## Prerequisite: Install Ubuntu with WSL first

Before you can install Vim with these instructions, you need to have **Ubuntu
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

## Step 3: Install Vim

Now that your Ubuntu system is updated, installing Vim is super easy!

In your Ubuntu terminal, type this command and press Enter:

```bash
sudo apt install vim
```

When it asks `(Y/n)`, type `Y` and press Enter to say "Yes, install it!"

## Step 4: Verify Your Installation

Let's make sure Vim is ready to go!

In your Ubuntu terminal, type this command and press Enter:

```bash
vim --version
```

You should see lots of information about Vim, including its version number. As
long as you see some text and a version, Vim is installed correctly!

Congratulations! Vim is now installed on your Windows computer, inside your
Ubuntu Linux system. You're ready to learn its secrets!

## Navigation

- Previous:
  [Chapter 01: Installing Vim on Linux (Arch)](@/ttk/install-vim/01-linux-arch.md)
- Next: [Chapter 03: Installing Vim on macOS](@/ttk/install-vim/03-macos.md)
