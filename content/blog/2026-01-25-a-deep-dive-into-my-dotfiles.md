+++
date = 2026-01-25
title = "A Deep Dive Into My Dotfiles: Crafting a CLI-First Workflow"
description = "A guided tour of my personal dotfiles repository, explaining the philosophy, tools, and configurations I use to create a fast, efficient, and keyboard-driven development environment on Arch Linux."
[taxonomies]
tags = ["dotfiles", "neovim", "hyprland", "arch linux", "cli", "workflow", "shell", "lua", "rust"]
+++

In my last post, I mentioned that a primary reason for my blogging hiatus was a
deep, obsessive dive into crafting my perfect development environment. Today, I
want to take you on a guided tour of that project: my personal
[dotfiles repository](https://github.com/mxaddict/dotfiles).

This repository is more than just a collection of config files; it's the
culmination of hundreds of hours spent refining a workflow that is fast,
keyboard-driven, and tailored to my needs as a developer who lives on the
command line.

### The Philosophy: Automation and Control

The core philosophy behind my dotfiles is simple: automate everything possible
while maintaining full control over my environment. I wanted a setup that I
could replicate on any machine with a single command, ensuring consistency and
saving hours of manual configuration. This is achieved through a combination of
custom shell scripts (`.deps` for installing dependencies, `.update` for setup)
and `GNU Stow` for elegantly managing symlinks.

### A Guided Tour of Key Components

Let's walk through some of the most important parts of my setup.

#### The Operating System: Arch Linux

The foundation of my setup is Arch Linux. I embrace its "do-it-yourself" ethos,
as it forces a deeper understanding of the system and allows for a truly
minimalist installation where I control every package. This lean and mean base
is the perfect canvas for a custom environment.

#### My Hardware: Laptops and Desktops

My dotfiles are designed to be portable, and I use them across two main
machines. For on-the-go work, I use a ThinkPad X13 Gen 2i. It's a fantastic,
reliable laptop that's great for travel, and surprisingly power-efficient. My
Hyprland + Neovim workflow, even when interacting with tools like `gemini-cli`,
typically consumes a mere 3-5 watts. With its 54Wh battery, this translates to
excellent real-world endurance; I managed to code my entire migration from
Jekyll to Zola and write all my new articles on a single charge. This kind of
battery performance is a testament to the efficiency of a well-tuned Linux
system with a minimalist setup.

My main desktop PC, however, is where the real power is. It's an all-AMD build
(X870E Nova WiFi motherboard), featuring a Ryzen 9 9950X3D CPU and a Radeon RX
7900 XTX GPU, with 64GB of RAM. I specifically chose this all-AMD setup for its
excellent open-source driver support on Linux. There are no proprietary drivers
to wrestle with, which makes for a stable, hassle-free experience, especially
when running a cutting-edge setup like mine.

#### The Desktop: Hyprland on Wayland

For my graphical environment, I've fully committed to the Wayland ecosystem with
[Hyprland](https://hyprland.org/) as my window manager. As a dynamic tiling
Wayland compositor, it's incredibly fluid and highly customizable. My
configuration is modular, sourcing separate files for monitors and workspaces to
keep things organized.

At launch, a suite of `exec-once` commands brings the environment to life,
starting essentials like `hyprpaper` for wallpaper, `waybar` for my status bar,
`swaync` for notifications, and `hypridle` for idle management. I use the
`dwindle` layout, which provides a predictable and efficient tiling structure.

The entire setup is designed to be keyboard-driven, minimizing the need to ever
touch a mouse. I have a set of custom keybindings using `$mod` (the Super key)
for everything from launching applications to managing windows:

```bash
# Launch a browser
bind = $mod, b, exec, vieb

# Launch a terminal
bind = $mod, c, exec, alacritty

# Kill active window
bind = $mod, q, killactive,

# Toggle floating window
bind = $mod, v, togglefloating,

# Move focus with mod + hjkl keys
bind = $mod, h, movefocus, l
bind = $mod, l, movefocus, r
bind = $mod, k, movefocus, u
bind = $mod, j, movefocus, d

# Switch workspaces with mod + [0-9]
bind = $mod, 1, workspace, 1
bind = $mod, 2, workspace, 2
bind = $mod, 3, workspace, 3
```

This level of customization is what makes Hyprland so powerful. It allows me to
craft an environment that is a true extension of my workflow, where every action
is just a few keystrokes away. The theme is a simple `adw-gtk3-dark` with
Papirus icons, keeping things clean and focused.

#### The Editor: Neovim on a LazyVim Base

As an avid `vim` user for years, the natural evolution for me was
[Neovim](https://neovim.io/). My configuration, which you can find in the repo,
has been fully migrated to Lua. The foundation of my setup is
[LazyVim](https://www.lazyvim.org/), a fantastic Neovim distribution that
provides a sensible, feature-rich baseline with a focus on lazy-loading plugins
for optimal performance.

On top of this solid base, I layer my own customizations. A great example of
this is how I enable specific features and language support via my
`lazyvim.json`. This allows me to precisely tailor the editor to the languages
and tools I use most frequently:

```json
{
    "extras": [
        "lazyvim.plugins.extras.coding.luasnip",
        "lazyvim.plugins.extras.coding.yanky",
        "lazyvim.plugins.extras.editor.telescope",
        "lazyvim.plugins.extras.formatting.prettier",
        "lazyvim.plugins.extras.lang.clangd",
        "lazyvim.plugins.extras.lang.docker",
        "lazyvim.plugins.extras.lang.git",
        "lazyvim.plugins.extras.lang.json",
        "lazyvim.plugins.extras.lang.markdown",
        "lazyvim.plugins.extras.lang.php",
        "lazyvim.plugins.extras.lang.python",
        "lazyvim.plugins.extras.lang.rust",
        "lazyvim.plugins.extras.lang.sql",
        "lazyvim.plugins.extras.lang.vue",
        "lazyvim.plugins.extras.lang.yaml",
        "lazyvim.plugins.extras.linting.eslint"
    ]
}
```

This approach gives me the best of both worlds: a powerful, pre-configured setup
from LazyVim that's easy to extend and personalize for my specific development
needs, all while keeping the configuration clean and manageable.

#### The Shell and CLI Tools

The command line is my home. My shell of choice is
[Fish](https://fishshell.com/), prized for its smart autocompletions and
user-friendly scripting. My setup is built around a suite of aliases and
functions that accelerate common tasks, removing friction from my daily
workflow. Every tool is chosen for its efficiency and command-line interface.

For example, I have a set of aliases to make Git interactions faster and more
fun. Instead of typing out a full commit command, I can just use `g` or `gg`,
which also pipes in a random quote from my `quoty` tool:

```fish
# Alias for quick and dirty git commit
function g
    git commit -am "$(quoty)"
    git pull --no-edit
    git push
end
function gg
    git add . && git commit -m "$(quoty)"
    git pull --no-edit
    git push
end
```

I also replace common commands with more modern, powerful alternatives. For
instance, `ls` is replaced with `eza`, a more feature-rich file lister:

```fish
# Replace default ls command with eza
function ls
    eza --group-directories-first $argv
end
```

And of course, no terminal-centric user would be complete without ensuring every
possible editor command opens their one true editor:

```fish
# I want v to open vi and vi to open vim
function n; nvim $argv; end
function v; nvim $argv; end
function vi; nvim $argv; end
# ...and so on
```

These small customizations, when combined, create a development environment that
is not only powerful but also deeply personal and efficient. This CLI-first
approach is a recurring theme throughout the repository.

#### Management with GNU Stow

Instead of having symlinks scattered everywhere, I use `GNU Stow` to manage my
dotfiles. This allows me to keep all my configurations neatly organized in a
version-controlled directory, and then "stow" them into their correct locations
in my home directory. It makes managing and updating the configurations
incredibly clean and simple.

### Why This Matters

Investing time in your dotfiles is an investment in yourself. A well-crafted
development environment reduces friction, automates mundane tasks, and
ultimately makes the process of creating software more enjoyable and efficient.
It's the digital equivalent of a perfectly organized workshop.

### Final Thoughts

This dotfiles project was the creative outlet I needed during my break from
writing. It allowed me to focus on building and refining the very tools I use to
create. I encourage you to explore my
[dotfiles repository on GitHub](https://github.com/mxaddict/dotfiles). Feel free
to take inspiration, fork it, and start your own journey toward crafting your
perfect development environment.
