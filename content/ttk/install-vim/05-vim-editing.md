+++
date = 2026-02-09
title = "Chapter 05: Vim Basics: Editing Your Code (Insert Mode)"
description = "For young learners! Learn how to switch to insert mode in Vim (i, a, o) to start writing and changing your code."
[taxonomies]
tags = ["vim", "editor", "cli", "tutorial", "education", "kids", "children", "young", "learners", "ttk", "vim basics", "editing", "insert mode"]
+++

Hello, Vim Editor!

You've mastered moving around in Vim's Normal Mode. That's fantastic! But to
actually change or write new code, you need to switch into a different mode
called **Insert Mode**. Think of Insert Mode as your "typing mode" – this is
where your keyboard keys actually type letters onto the screen.

## Switching to Insert Mode: Your Typing Spells

There are a few magical ways to enter Insert Mode from Normal Mode:

- **`i`**: The most common spell! Press `i` to enter Insert Mode _before_ your
  cursor.
- **`a`**: Press `a` (for "append") to enter Insert Mode _after_ your cursor.
- **`o`**: Press `o` (for "open") to create a _new line below_ your current line
  and enter Insert Mode there.
- **`O` (capital O)**: Press `O` to create a _new line above_ your current line
  and enter Insert Mode there.

When you are in Insert Mode, you will usually see `-- INSERT --` at the bottom
of your Vim window. This is a very important sign that you can start typing!

## Going Back to Normal Mode: The Escape Key

When you're done typing and want to move around again or use other Vim commands,
you need to go back to Normal Mode.

- Press the **`Escape`** key (usually `Esc` in the top-left corner of your
  keyboard).

As soon as you press `Escape`, `-- INSERT --` will disappear from the bottom,
and you'll be back in Normal Mode, ready to use your movement spells!

## Deleting with Spells: `dd`, `x`

You can also delete things without going into Insert Mode, directly from Normal
Mode!

- **`dd`**: This powerful spell will delete the _entire line_ your cursor is on.
  (Type `d` twice quickly!)
- **`x`**: This spell will delete the _single character_ under your cursor.

## Copying and Pasting (Yank and Put!): `yy`, `p`

Vim has its own special words for copy and paste!

- **`yy`**: (for "yank") This spell will copy the _entire line_ your cursor is
  on. (Type `y` twice quickly!)
- **`p`**: (for "put") This spell will paste the copied line _below_ your
  current line.

## Putting it Together: Practice Time

1. Open a text file with Vim (`vim practice.txt`).
2. Press `Escape` to ensure you're in Normal Mode.
3. Use your movement spells (`h`, `j`, `k`, `l`, `w`, `b`, `0`, `$`) to move
   your cursor around.
4. Press `i` to enter Insert Mode. Type some words!
5. Press `Escape` to go back to Normal Mode.
6. Move your cursor to a different spot.
7. Press `a` to enter Insert Mode. Type some more words!
8. Press `Escape`.
9. Move your cursor to the middle of a line and press `x` a few times to delete
   characters.
10. Move your cursor to a line and press `dd` to delete the whole line.
11. Type `o`, enter Insert Mode, type a new sentence, then `Escape`.
12. With your cursor on a line, type `yy` to copy it.
13. Move to a new line and press `p` to paste it!

You're now learning to both move around _and_ edit your code in Vim. Awesome
job, Code Wizard!

## Navigation

- Previous:
  [Chapter 04: Vim Basics: Moving Around Like a Pro](@/ttk/install-vim/04-vim-movement.md)
- Next:
  [Chapter 06: Vim Basics: Saving Your Work and Exiting](@/ttk/install-vim/06-vim-saving-exiting.md)
