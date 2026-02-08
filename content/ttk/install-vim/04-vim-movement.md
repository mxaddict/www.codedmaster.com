+++
date = 2026-02-09
title = "Chapter 04: Vim Basics: Moving Around Like a Pro"
description = "For young learners! Master the fundamental movements in Vim (h, j, k, l) to navigate your code quickly and efficiently."
[taxonomies]
tags = ["vim", "editor", "cli", "tutorial", "education", "kids", "children", "young", "learners", "ttk", "vim basics", "movement"]
+++

Hello, Vim Explorer!

Now that you have Vim installed, it's time to learn its first secret: how to
move around! In Vim, you don't use your mouse much. Instead, you use special
keys on your keyboard to zip around your code super fast!

## Normal Mode: Your Control Center

When you first open Vim, you are in **Normal Mode**. Think of this as your
"control center" or "reading mode." In this mode, the keys on your keyboard
aren't for typing words; they're for giving commands to Vim!

To make sure you're in Normal Mode, just press the `Escape` key (usually in the
top-left corner of your keyboard).

## Basic Movement Spells: H, J, K, L

These four keys are like your Vim game controller! They're right under your
fingers when your hands are on the keyboard's "home row."

- **`h`**: Move **Left** (like an arrow pointing left)
- **`j`**: Move **Down** (like an arrow pointing down)
- **`k`**: Move **Up** (like an arrow pointing up)
- **`l`**: Move **Right** (like an arrow pointing right)

Try it out! Open a file with Vim (for example, `vim test.txt`) and try pressing
`h`, `j`, `k`, `l` a few times. Watch your cursor jump around!

## Faster Movement Spells: W and B (Word Jumps!)

Moving one letter at a time is good, but sometimes you want to move faster, like
jumping whole words!

- **`w`**: Jump to the **W**ord beginning (moves your cursor to the beginning of
  the _next_ word).
- **`b`**: Jump **B**ack to the beginning of the _previous_ word.

Try these too! Press `w` repeatedly to jump forward word by word. Then press `b`
to jump backward.

## End of Line and Start of Line Spells: 0 and $

What if you want to go to the very beginning or very end of a line of code?

- **`0` (zero)**: Go to the very beginning of the current line.
- **`$`**: Go to the very **E**nd of the current line.

These are super handy for quick fixes!

## Putting it Together: Practice Time

Open any text file with Vim (you can even make a new one by just typing
`vim practice.txt` and pressing Enter). Now, try these moves:

1. Press `Escape` to make sure you're in Normal Mode.
2. Use `j` and `k` to move up and down lines.
3. Use `h` and `l` to move left and right characters.
4. Jump with `w` and `b`.
5. Go to the start of a line with `0`.
6. Go to the end of a line with `$`!

You're already becoming a Vim movement master! This is just the beginning of how
fast you can navigate your code.

## Navigation

- Previous: [Chapter 03: Installing Vim on macOS](@/ttk/install-vim/03-macos.md)
- Next:
  [Chapter 05: Vim Basics: Editing Your Code (Insert Mode)](@/ttk/install-vim/05-vim-editing.md)
