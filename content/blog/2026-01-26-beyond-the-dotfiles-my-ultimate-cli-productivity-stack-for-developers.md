+++
date = 2026-01-26
title = "Beyond the Dotfiles: My Ultimate CLI Productivity Stack for Developers"
description = "Discover how a curated set of command-line tools and configurations can transform your development workflow into a hyper-efficient, keyboard-driven experience."
[taxonomies]
tags = ["cli", "productivity", "workflow", "dotfiles", "linux", "hyprland", "neovim", "fish", "tmux", "rust", "automation"]
+++

## Introduction

In the demanding world of software development, efficiency isn't just a luxury;
it's a necessity. The constant dance between coding, debugging, testing, and
deploying often leads to context switching, repetitive tasks, and a drain on
mental energy. For many, the graphical user interface (GUI) can become a source
of friction, slowing down interactions and pulling focus away from the core
task.

This article isn't just about my personal `.files` repository (though you can
explore it [on GitHub](https://github.com/mxaddict/dotfiles) if you're curious).
Instead, it's about the philosophy and practical application of a "CLI
Productivity Stack" – a meticulously curated collection of command-line tools
and configurations that transforms the humble terminal into a hyper-efficient,
keyboard-driven development hub.

My journey to this setup was born out of a desire to eliminate friction,
maximize focus, and make every interaction with my system as fast and intuitive
as possible. The goal was to create an environment where my thoughts could flow
directly into code, unhindered by unnecessary clicks or cumbersome interfaces.

Throughout this guide, you'll discover how I've leveraged tools like Fish Shell,
Neovim, Hyprland, and Tmux, alongside a host of purpose-built utilities, to
streamline every aspect of my daily development. You'll learn about:

- **The foundational components:** How a well-tuned terminal, shell, and window
  manager provide a solid base.
- **Core workhorses:** Specific command-line tools that revolutionize file
  navigation, code editing, and Git workflows.
- **Automation and customization:** Techniques to make your environment truly
  your own, reducing repetitive tasks to single keystrokes.

By the end, you'll have a blueprint to inspire your own journey toward a more
productive, enjoyable, and command-line-centric development experience.

## The Foundational Layer: Your Shell & Terminal (The "Home Base")

The journey to a truly efficient command-line workflow begins with a robust
foundation. This involves selecting and meticulously configuring the core
components that dictate how you interact with your system: your terminal
emulator, your shell, and your window manager. Each choice here significantly
impacts speed, comfort, and overall productivity.

### Terminal Emulator: Alacritty – Blazing Fast and Minimalist

At the heart of my CLI setup is [Alacritty](https://alacritty.org/), a
GPU-accelerated terminal emulator. While many excellent options exist, Alacritty
stands out for its uncompromising focus on speed and minimalism. It's built with
Rust, which aligns perfectly with my preference for performance-oriented tools.

Unlike some terminals, Alacritty delegates rendering to the GPU, offering a
silky-smooth, low-latency experience that feels incredibly responsive, even with
complex output. My configuration for Alacritty is straightforward, emphasizing
readability and speed, complementing the rest of my streamlined environment.

### Shell: Fish – The Friendly Interactive SHell

For my shell, I've chosen [Fish](https://fishshell.com/) (the Friendly
Interactive SHell) over more traditional options like Bash or Zsh. Fish is
designed for the user, offering powerful features out-of-the-box that would
require extensive configuration in other shells:

- **Smart Autocompletions:** Context-aware suggestions appear as you type,
  learning from your history and system commands. This drastically reduces
  typing and improves recall.
- **Syntax Highlighting:** Commands are highlighted as you type, immediately
  identifying errors or valid syntax.
- **User-friendly Scripting:** Fish's scripting language is cleaner and more
  intuitive than Bash, making it easier to automate tasks.

My `config.fish` is a testament to Fish's extensibility and my drive for
customization:

- **Path Management:** Meticulously configured `fish_add_path` ensures all my
  binaries from Cargo, local scripts, Composer, Neovim Mason, and Homebrew are
  always accessible.
- **Pagers and `cat` replacement:** Both `PARU_PAGER` and `MANPAGER` are set to
  utilize `bat` (the `cat` replacement with syntax highlighting and Git
  integration). In fact, I've aliased `cat` itself to `bat --plain`, making even
  simple file viewing more pleasant.
- **`eza` as `ls` and `tree`:** I've replaced the venerable `ls` command with
  `eza`, a modern, feature-rich alternative that offers better defaults, Git
  integration, and icons. My `config.fish` includes aliases like `ls`, `l`,
  `la`, `ll` to `eza` with various flags, and `tree` is aliased to `eza --tree`.

```fish
# Replace default ls command with eza
function ls
    eza --group-directories-first $argv
end

# Replace tree command with eza
function tree
    eza --tree $argv
end

# Some more ls
function l
    ls -lF $argv
end
function la
    ls -aF $argv
end
function ll
    ls -alF $argv
end

# Replace cat with bat
function cat
    bat --plain $argv
end
```

### Prompt: Starship – The Cross-Shell Prompt

To maintain a consistent and information-rich prompt across different shell
environments (though predominantly Fish for me), I use
[Starship](https://starship.rs/). Written in Rust, Starship is incredibly fast
and customizable, providing immediate feedback on my current Git status, Rust
toolchain, Node.js version (managed by `fnm`), and more, directly in the prompt.
It's configured to be concise yet informative, minimizing visual clutter while
providing critical context at a glance.

### Multiplexer: Tmux – Terminal Session Management

For managing multiple terminal sessions, panes, and windows within a single
terminal emulator instance, [Tmux](https://github.com/tmux/tmux/wiki) is
indispensable. It allows me to detach from sessions and reattach later, keep
server processes running in the background, and effortlessly switch between
development tasks.

My `tmux.conf` (configured via `tpm`, the Tmux Plugin Manager) creates a
persistent, organized workspace. Crucially, I integrate Tmux with Neovim using
the `christoomey/vim-tmux-navigator` plugin. This allows me to seamlessly
navigate between Neovim splits and Tmux panes using the _same_ keybindings
(`Ctrl-h`, `Ctrl-j`, `Ctrl-k`, `Ctrl-l`), eliminating context-switching
friction:

```lua
-- nvim/lua/plugins/tmux.lua
return {
  "christoomey/vim-tmux-navigator",
  cmd = {
    "TmuxNavigateLeft",
    "TmuxNavigateDown",
    "TmuxNavigateUp",
    "TmuxNavigateRight",
    "TmuxNavigatePrevious",
    "TmuxNavigatorProcessList",
  },
  keys = {
    { "<c-h>", "<cmd><C-U>TmuxNavigateLeft<cr>" },
    { "<c-j>", "<cmd><C-U>TmuxNavigateDown<cr>" },
    { "<c-k>", "<cmd><C-U>TmuxNavigateUp<cr>" },
    { "<c-l>", "<cmd><C-U>TmuxNavigateRight<cr>" },
    { "<c-\">", "<cmd><C-U>TmuxNavigatePrevious<cr>" },
  },
}
```

This integration means my hands rarely leave the home row, maintaining flow
whether I'm traversing code in Neovim or checking logs in an adjacent Tmux pane.

### Window Manager: Hyprland – A Keyboard-Driven Wayland Desktop

Moving beyond the terminal, my entire graphical environment is built around
[Hyprland](https://hyprland.org/), a dynamic tiling Wayland compositor. Hyprland
provides an incredibly fluid, GPU-accelerated desktop experience that is almost
entirely keyboard-driven. It's highly customizable and allows for precise
control over window placement and behavior.

Key aspects of my Hyprland configuration that enhance productivity include:

- **Tiling Layout (`dwindle`):** Windows are automatically arranged in a
  non-overlapping fashion, maximizing screen real estate and reducing manual
  window management.
- **Workflow Optimization:** Disabling animations
  (`animations { enabled = false }`) ensures a snappy, distraction-free
  experience.
- **Extensive Keybindings:** My `hyprland.conf` is a dense map of custom
  keybindings using the Super key (`$mod`):
  - **Application Launching:** Single keystrokes to open `alacritty`
      (terminal), `vieb` (browser), `nautilus` (file manager).
  - **Window Management:** Easily kill active windows (`$mod, q`), toggle
      floating mode (`$mod, v`), or fullscreen (`$mod, f`).
  - **Window and Focus Navigation (`$mod + hjkl`):** Just like in Vim and
      Tmux, `hjkl` are used to move focus between windows and
      `$mod + Shift + hjkl` to move windows themselves, creating a cohesive
      navigation experience across the entire system.
  - **Workspace Management:** Dedicated keybindings for switching between and
      moving windows to 10 distinct workspaces, allowing for highly organized
      task separation (e.g., all communication apps on Workspace 2, crypto
      wallets on Workspace 7).
  - **Integrated Utilities:** Keybindings for `hyprlock` (screen lock),
      `grimblast` (screenshots with automatic timestamping), `hyprpicker` (color
      picker), and `kooha` (screen recorder).
  - **Custom Menus and Scripts:** A suite of binds to `~/.local/bin/.menu-*`
      scripts (`.menu-power`, `.menu-apps`, `.menu-calc`, etc.) and even
      autofill/password management (`~/.local/bin/.menu-autofill`) –
      transforming complex actions into simple key combinations.

```ini
# Excerpt from ~/.config/hypr/hyprland.conf

# Browser
bind = $mod, b, exec, vieb

# Terminal
bind = $mod, c, exec, alacritty

# File manager
bind = $mod, e, exec, nautilus -w

# Lock screen
bind = $mod, m, exec, hyprlock

# Move focus with mod + hjkl keys
bind = $mod, h, movefocus, l
bind = $mod, l, movefocus, r
# ... (rest of the hjkl binds)

# Switch workspaces with mod + [0-9]
bind = $mod, 1, workspace, 1
# ... up to 10
```

This cohesive setup, from the terminal emulator to the window manager, forms the
unbreakable core of my productivity, ensuring that my environment is always
working _for_ me, not against me.

## Core Productivity Pillars: Tools for Specific Tasks (The "Workhorses")

With a solid foundational layer in place, the next step is to equip your
command-line environment with specialized tools that excel at common development
tasks. These "workhorse" utilities are chosen for their speed, efficiency, and
seamless integration into a CLI-first workflow.

### A. File Navigation & Exploration

Navigating complex project structures and finding specific files quickly is
paramount for developer productivity. My stack replaces slower, traditional
tools with modern, blazingly fast alternatives.

- **`eza` (Enhanced `ls`):** As seen in my `config.fish`, `eza` has completely
  replaced the venerable `ls`. It provides beautiful, informative output with
  Git integration, file type icons, and an intuitive tree view. This makes
  scanning directories and understanding repository status significantly faster.
- **`fd` (Fast Directory Entry):** This is a faster and more user-friendly
  alternative to `find`. Written in Rust, `fd` understands `.gitignore` by
  default and offers a simpler, more intuitive syntax for searching files and
  directories. When combined with `fzf`, it creates an incredibly powerful
  search mechanism.
- **`zoxide` (Smarter `cd`):** Navigating deeply nested directories is a thing
  of the past with `zoxide`. It's a smart `cd` command that learns your most
  used directories. Simply typing `z <part_of_directory_name>` instantly jumps
  you to the most relevant frequently visited directory, drastically reducing
  keystrokes and context switching.
- **`fzf` (Fuzzy Finder):** The ultimate fuzzy finder for the command line.
  `fzf` integrates with almost any command that outputs a list. In my setup,
  it's used extensively:
  - **File Selection:** Chained with `fd` to quickly find and open files.
  - **Command History:** Instantly search and execute past commands.
  - **Process Management:** Find and kill processes.
  - **Git Integration:** Search Git commits, files in history, or branches.

My `config.fish` includes extensive `FZF_DEFAULT_OPTS` for theming and layout,
ensuring a visually consistent and efficient fuzzy-finding experience. It also
uses `bat` for file previews directly within `fzf`:

```fish
# FZF theme
set -gx FZF_CTRL_T_OPTS "--preview 'bat -n --color=always {}'"
set -gx FZF_DEFAULT_OPTS "$FZF_DEFAULT_OPTS" \
    --height 100%
    --info=inline-right
    --ansi
    --layout=reverse
    --border=none
    --color=bg+:#283457
    --color=bg:#16161e
    --color=border:#27a1b9
    --color=fg:#c0caf5
    --color=gutter:#16161e
    --color=header:#ff9e64
    --color=hl+:#2ac3de
    --color=hl:#2ac3de
    --color=info:#545c7e
    --color=marker:#ff007c
    --color=pointer:#ff007c
    --color=prompt:#2ac3de
    --color=query:#c0caf5:regular
    --color=scrollbar:#27a1b9
    --color=separator:#ff9e64
    --color=spinner:#ff007c
```

This level of customization transforms `fzf` from a simple tool into a powerful,
integrated navigation hub.

### B. Code Editing & IDE Replacement

While the terminal provides the command center, the code editor is where the
actual development happens. For a CLI-first workflow, this means a powerful,
keyboard-driven editor that can stand toe-to-toe with any graphical IDE.

- **Neovim (with LazyVim):** My editor of choice is
  [Neovim](https://neovim.io/), a highly extensible, terminal-based editor.
  Built upon a robust Lua-based configuration, my setup leverages
  [LazyVim](https://www.lazyvim.org/) as a solid, performant foundation. LazyVim
  provides intelligent defaults and lazy-loads plugins, ensuring Neovim remains
  incredibly fast and responsive.
  - **Language Server Protocol (LSP) Integration:** Through LazyVim's extras,
      I have comprehensive language support for a wide array of languages
      including Python, Rust, PHP (with Intelephense), JavaScript/TypeScript
      (with ESLint), Docker, SQL, and more. This provides features like
      auto-completion, go-to-definition, refactoring, and linting—all within the
      terminal.
  - **Keyboard-Driven Efficiency:** Neovim's modal editing paradigm, combined
      with custom keybindings and plugins like `telescope` (for fuzzy finding
      files, symbols, and commands) and `luasnip` (for code snippets), ensures
      that my hands rarely leave the keyboard, maintaining peak flow state.
  - **Tmux-Neovim Navigation:** As highlighted in the "Multiplexer" section,
      the seamless navigation between Neovim splits and Tmux panes using
      `Ctrl-h/j/k/l` further solidifies the keyboard-driven experience, making
      the entire environment feel like one giant, integrated IDE.
  - **Fine-tuned Customization:** My `nvim/lua/config/options.lua`
      demonstrates a preference for speed and efficiency, such as disabling
      animations (`vim.g.snacks_animate = false`).

### C. Git Workflow Enhancement

Version control is an indispensable part of software development, and the
command line offers the most powerful and granular control over Git. My workflow
enhances this power with tools designed to make Git operations faster, more
intuitive, and even more enjoyable.

- **`Quoty` (for better commit messages):** One of the common pitfalls in Git
  history is vague or uninspired commit messages. To combat this, I developed
  `quoty`, a Rust-based CLI tool that injects a random, often insightful,
  programmer quote directly into my commit messages. This ensures every commit
  is at least memorable, if not deeply profound. My `config.fish` includes
  custom aliases that integrate `quoty` directly into my commit workflow:

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

    These aliases streamline the entire commit-push cycle, reducing it to a
    single command while ensuring commit messages are never "Updates" or "Fixes"
    again.

- **`lazygit` (Interactive Git UI):** For more complex Git operations like
  interactive rebasing, staging specific lines, or quickly reviewing diffs,
  `lazygit` provides a fantastic terminal user interface (TUI). It bridges the
  gap between the raw power of Git CLI and the visual feedback of a GUI,
  allowing me to perform sophisticated Git tasks with intuitive keybindings and
  a clear overview of my repository state. A simple `lg` alias in my shell
  launches it instantly.

### D. Search & Grepping

Efficiently finding information within your codebase is a cornerstone of
productivity. Whether it's locating a function definition, tracking down a
variable, or simply remembering where a particular string was used, quick and
accurate search tools are invaluable. My stack relies on highly optimized,
Rust-based utilities that deliver speed and intelligence far beyond traditional
`grep` and `find`.

- **`ripgrep` (`rg`):** This is my go-to tool for searching code. `ripgrep` is a
  line-oriented search tool that recursively searches the current directory for
  a regex pattern. It's blazingly fast because it's built in Rust, respects
  `.gitignore` rules by default, and intelligently skips binary files. Its
  output is clean and easy to parse, making it far superior to `grep` for most
  development tasks.
- **`fd` (Fast Directory Entry / Find):** While already mentioned in "File
  Navigation & Exploration" for finding files, `fd` also plays a crucial role
  here. It's often piped to `ripgrep` to perform highly targeted searches across
  specific file types or within certain directories. For example,
  `fd .js | rg 'myFunction'` quickly searches for `myFunction` only within
  JavaScript files, combining the strengths of both tools.

The combination of `ripgrep` and `fd`, often orchestrated with `fzf`, creates an
incredibly powerful and flexible search system that makes navigating even the
largest codebases a breeze.

## Automation & Customization: Making it Your Own

The true power of a CLI productivity stack lies not just in the individual
tools, but in how they are seamlessly integrated and automated to fit your
unique workflow. This is where the "Making it Your Own" philosophy comes into
play, transforming repetitive tasks into single commands and tailoring your
environment to your exact needs.

### Shell Scripting: Your Personal Automation Engine

My `.files` repository is filled with custom shell scripts, primarily in Fish,
that serve as my personal automation engine. These scripts range from simple
aliases to complex workflows that orchestrate multiple commands.

- **Setup and Update Scripts (`.deps`, `.update`):** At the foundation are my
  `.deps` and `.update` scripts. `.deps` (short for dependencies) handles the
  cross-platform installation of all core tools, using `paru` on Arch, `brew` on
  macOS, and `apt-get` on Debian/Ubuntu. This ensures my environment is
  consistently provisioned across different machines. The `.update` script then
  takes over, pulling the latest dotfiles, applying `GNU Stow`, updating plugins
  for Neovim and Tmux, and configuring system-level settings. These two scripts
  embody the principle of "infrastructure as code" for my personal setup.
- **Custom Menus (`.menu-apps`, `.menu-power`, etc.):** As seen in my Hyprland
  configuration, a suite of `~/.local/bin/.menu-*` scripts provide quick,
  interactive menus for launching applications, managing power, selecting Wi-Fi
  networks, and even performing calculations. These are typically driven by
  `rofi`, offering a fast, keyboard-driven alternative to traditional GUI menus.
- **Autofill and Password Management (`.menu-autofill`):** A standout example of
  deep integration is the `.menu-autofill` script. Bound to
  `Ctrl+Mod+j/k/l/semicolon`, it provides secure autofill functionality for
  authentication, usernames, passwords, and one-time passwords, streamlining
  login processes across various applications and websites without ever touching
  a mouse.

### `GNU Stow`: Elegant Dotfile Management

Managing configuration files across multiple machines or even just keeping them
organized in a version control system can be a challenge. I use `GNU Stow` for
elegant dotfile management. Instead of littering my home directory with
symlinks, `Stow` treats each top-level directory in my `.files` repository
(e.g., `fish`, `nvim`, `hypr`) as a separate package. When "stowed," it creates
symbolic links from these packages into the appropriate locations in my home
directory. This makes adding, removing, or updating configurations incredibly
clean and transparent.

### Keybinding Philosophy: Muscle Memory and Consistency

A central tenet of my CLI productivity stack is a consistent, comprehensive
keybinding philosophy. The goal is to reduce cognitive load and build muscle
memory, so common actions become second nature.

- **Vim-like Navigation Everywhere:** The `hjkl` keys, the cornerstone of Vim's
  navigation, are consistently used across Neovim, Tmux, and Hyprland for moving
  focus and windows. This creates a unified spatial understanding of the
  environment.
- **Global Hotkeys:** Important actions are mapped to global hotkeys (often
  involving the Super key, `$mod`, in Hyprland) for instant access. This
  includes application launching, window management, and utility functions like
  screenshots and screen recording.
- **Logical Grouping:** Keybindings are grouped logically (e.g.,
  `Ctrl+Mod+j/k/l/semicolon` for autofill, `Mod+1-0` for workspaces), making
  them easier to remember and use.

This deliberate approach to keybindings ensures that every interaction feels
natural and immediate, empowering a truly keyboard-driven workflow that
minimizes distractions and maximizes focus.

## Conclusion

Building an ultimate CLI productivity stack is an ongoing journey of refinement
and customization. It's about more than just a collection of tools; it's a
philosophy that prioritizes efficiency, consistency, and a deep understanding of
your own workflow. By investing time in customizing your terminal, shell,
editor, and window manager, you create an environment that actively supports
your focus and accelerates your development.

We've explored how a carefully chosen set of tools – from Alacritty and Fish to
Neovim, Tmux, and Hyprland – can transform mundane tasks into fluid,
keyboard-driven operations. We've seen how `eza`, `fd`, `zoxide`, `fzf`,
`ripgrep`, and `lazygit` elevate file navigation, search, and Git management to
new heights. And crucially, we've highlighted the power of custom scripting and
`GNU Stow` in automating your environment, alongside a consistent keybinding
philosophy that builds muscle memory and reduces cognitive load.

This is not a static setup, but a living, evolving system designed to adapt to
new challenges and continuously improve. I encourage you to explore the tools
mentioned, experiment with your own configurations, and embark on your own
journey to craft a CLI productivity stack that truly works for you. The command
line is a powerful ally; master it, and you'll unlock a new level of development
efficiency and enjoyment.
