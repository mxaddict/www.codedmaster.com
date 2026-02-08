+++
date = 2026-02-09
title = "Chapter 01: Getting Started with WSL"
description = "For young learners! A step-by-step guide to enabling Windows Subsystem for Linux (WSL) on your Windows computer."
[taxonomies]
tags = ["wsl", "windows", "linux", "ubuntu", "installation", "tutorial", "education", "kids", "children", "young", "learners", "ttk", "enable wsl", "features"]
+++

Hello, Windows Adventurer!

This chapter will show you how to get the Windows Subsystem for Linux (WSL)
ready on your Windows computer. It's like flipping a switch to turn on a hidden
Linux superpower!

## Step 1: Open PowerShell as an Administrator

First, we need to open a special program called **PowerShell** with
"administrator" powers. This lets us make important changes to your computer.

1. Click on the **Windows Start button**.
2. Type "PowerShell".
3. You'll see "Windows PowerShell" or just "PowerShell" in the search results.
   **Right-click** on it.
4. Choose **"Run as administrator"**.
5. If a window pops up asking "Do you want to allow this app to make changes to
   your device?", click "Yes".

You'll see a blue window open – that's PowerShell!

## Step 2: Install WSL

Now for the magic command! This single command will do almost everything needed
to set up WSL for you.

In the PowerShell window, type this command exactly and press Enter:

```powershell
wsl --install
```

Your computer will start working! It will enable the necessary Windows features
and download the newest Ubuntu Linux distribution. This might take a few
minutes.

If your computer asks you to restart, **make sure to restart your computer**
when this step is finished. This is very important!

## Step 3: Check If WSL is Ready (After Restart, if needed)

After your computer restarts (if it asked you to), open PowerShell **again**
(you don't need to run as administrator this time).

Type this command and press Enter:

```powershell
wsl --list --online
```

This command shows you a list of different Linux versions you can install. If
you see a list, it means WSL is enabled and ready! Ubuntu is usually the default
one that `wsl --install` sets up.

Congratulations! WSL is now enabled on your Windows machine. Next, we'll set up
your Ubuntu Linux!

## Navigation

- Previous:
  [Install Ubuntu with WSL: Your Linux Adventure on Windows!](@/ttk/install-wsl/_index.md)
- Next:
  [Chapter 02: Setting Up Ubuntu in WSL](@/ttk/install-wsl/02-ubuntu-setup.md)
