+++
date = 2026-02-09
title = "Chapter 02: Installing Vim on Windows"
description = "For young learners! Learn how to install Vim, your powerful text editor, on your Windows computer."
[taxonomies]
tags = ["vim", "editor", "cli", "installation", "tutorial", "education", "kids", "children", "young", "learners", "ttk", "windows"]
+++

Hello, Windows Adventurer!

If you're using a computer with Windows, this chapter will show you how to
install Vim, your powerful text editor!

## Step 1: Download the Installer

Open your web browser (like Chrome, Edge, or Firefox) and go to the official Vim
website for Windows:

[**https://www.vim.org/download.php#pc**](https://www.vim.org/download.php#pc)

Look for a link that says something like "Self-installing executable" under
"MS-Windows". Click on the link for "gVim" (which is Vim with a graphical
interface, making it a bit easier to start). It will download a file named
something like `gvim82.exe` (the numbers might be different).

## Step 2: Run the Installer

Once the installer file has finished downloading, find it (usually in your
"Downloads" folder) and double-click it to run it.

Follow the instructions in the installer:

- Click "Yes" if it asks for permission.
- Click "Next" to start.
- Agree to the license terms.
- Choose where to install Vim (the default location is usually fine).
- **Important!** On the "Custom Setup" screen, make sure to check the box that
  says "Create Desktop Icon" and also "Install for all users" if you want
  everyone using the computer to have access. You might also see an option for
  "Install `_vimrc` for all users". It's good to check this too.
- Click "Install" and let it finish.
- Click "Finish" when it's done.

## Step 3: Verify Your Installation

Now, let's check if Vim is ready to go!

Open a **Command Prompt** or **PowerShell** window. You can find this by
searching for "cmd" or "PowerShell" in your Windows search bar.

Type this command into the Command Prompt/PowerShell window and press Enter:

```bash
vim --version
```

You should see lots of information about Vim, including its version number. As
long as you see some text and a version, Vim is installed correctly!

Congratulations! Vim is now installed on your Windows computer. Get ready to
learn its secrets!

## Navigation

- Previous:
  [Chapter 01: Installing Vim on Linux (Arch)](@/ttk/install-vim/01-linux-arch.md)
- Next: [Chapter 03: Installing Vim on macOS](@/ttk/install-vim/03-macos.md)
