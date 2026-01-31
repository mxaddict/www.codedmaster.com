+++
date = 2026-01-31
title = "Mastering Your Dotfiles: A Guide to a Cleaner Setup with Git and Stow"
description = "Discover a simplified, yet powerful method for managing your dotfiles across multiple machines. This guide walks you through creating a clean, easy-to-maintain dotfiles repository using Git and GNU Stow, helping you keep your development environment consistent and personalized."
[taxonomies]
tags = ["dotfiles", "git", "stow", "linux", "developer-tools", "productivity", "neovim", "fish", "bash"]
+++

In this tutorial / guide, I'll walk you through the process of setting up your
own dotfiles repository. This will allow you to keep track of your configuration
files, sync them across multiple machines, and share them with others. We will
be using `git` for version control and `GNU Stow` for symlinking the files.

## Step 1: Initialize Your Git Repository

First, you'll need to create a new directory for your dotfiles and initialize a
git repository within it.

```bash
mkdir ~/.files
cd ~/.files
git init
```

This will create a hidden `.files` directory in your home folder and initialize
an empty Git repository.

## Step 2: Add Your Dotfiles

Next, you'll want to move your existing dotfiles into the new repository.
Instead of creating subdirectories for each application, we'll mirror the
structure of your home directory directly within your `~/.files` repository.
This approach simplifies management by allowing you to place files exactly where
they would reside in your `$HOME` directory. For example, if you're adding your
`.bashrc`, your Neovim configuration (`~/.config/nvim`), and your Fish shell
configuration (`~/.config/fish/config.fish`), you might do the following:

```bash
mv ~/.bashrc ~/.files/.bashrc
mv ~/.config/nvim ~/.files/.config/nvim
mkdir -p ~/.files/.config/fish/ # Ensure the parent directory exists
mv ~/.config/fish/config.fish ~/.files/.config/fish/config.fish

```

This method ensures that the path inside your `~/.files` directory directly
corresponds to its target path in your `$HOME` directory. This means when Stow
creates symlinks, `~/.files/.bashrc` will link to `~/.bashrc`,
`~/.files/.config/nvim` will link to `~/.config/nvim`, and
`~/.files/.config/fish/config.fish` will link to `~/.config/fish/config.fish`.

## Step 3: Create an Update Script with Stow

Now, let's create a script that will use `GNU Stow` to create symlinks from your
home directory to the files in your dotfiles repository. This script will also
use `stow --adopt` to adopt any existing files that are already in your home
directory.

Create a file named `.update` in the root of your dotfiles repository with the
following content:

```bash
#!/bin/bash

# This script will adopt any existing dotfiles and then stow the new ones.
# The -R flag tells stow to re-stow the packages, which is what we want.
# The --adopt flag tells stow to move any existing files in the target directory
# into the stow directory if they are not already a symlink.

stow -R --adopt .
```

Make the script executable:

```bash
chmod +x .update
```

### Understanding `stow --adopt`

The `--adopt` flag is a crucial part of this setup. When you run
`stow --adopt .`, Stow looks at the packages in your dotfiles directory (in this
case, all of them). For each package, it checks your home directory (the
target). If it finds a file or directory that should be a symlink but is instead
a real file, it _adopts_ it by moving it into your dotfiles repository and then
creating the symlink.

This is extremely useful when you're first setting up your dotfiles repository,
as it allows you to move your existing configurations into the repository
without having to do it manually.

## Conclusion

You now have a fully functional dotfiles repository! You can add more dotfiles
as needed, commit your changes with `git`, and push them to a remote repository
like GitHub or GitLab. For an example of how this method can be used in the
wild, check out
[my dotfiles repository](https://www.github.com/mxaddict/dotfiles). When you set
up a new machine, you can simply clone your dotfiles repository and run the
`.update` script to get all your configurations in place.
