+++
date = 2026-02-09
title = "Chapter 06: Vim Basics: Saving Your Work and Exiting"
description = "For young learners! Learn the essential commands to save your changes (`:w`) and exit Vim (`:q`, `:wq`, `:q!`)."
[taxonomies]
tags = ["vim", "editor", "cli", "tutorial", "education", "kids", "children", "young", "learners", "ttk", "vim basics", "saving", "exiting"]
+++

Hello, Vim Finisher!

You've learned how to move and edit in Vim. That's super important! But what's
just as important is knowing how to **save your changes** and **leave Vim** when
you're done. Otherwise, all your hard work might disappear!

## Command Mode: Your Saving Spells

To save and exit in Vim, you need to be in a special mode called **Command
Mode**. You get there from **Normal Mode** by typing a colon (`:`). When you
type `:`, you'll see it appear at the bottom of your Vim window. This means Vim
is waiting for a command!

Remember: Always press `Escape` first to make sure you are in Normal Mode before
trying to enter Command Mode with `:`.

## Saving Your Changes: `:w`

- **`:w`**: (for "write") This spell tells Vim to save all the changes you've
  made to your file.
  - Type **`:`**
  - Then type **`w`**
  - Then press **`Enter`**

You'll see a message at the bottom, usually saying something like `filename.txt`
written, and how many lines and characters were saved.

## Exiting Vim: `:q`, `:wq`, `:q!`

Once you've saved your work, you'll want to close Vim.

- **`:q`**: (for "quit") This spell tells Vim to close the file.
  - Type **`:`**
  - Then type **`q`**
  - Then press **`Enter`**

  **Important:** This only works if you haven't made any changes since your last
  save. If you try to quit without saving, Vim will tell you:
  `No write since last change (add ! to override)`.

- **`:wq`**: (for "write and quit") This is a super handy spell! It saves your
  changes _and_ then quits Vim, all in one go!
  - Type **`:`**
  - Then type **`wq`**
  - Then press **`Enter`**

- **`:q!`**: (for "quit, forcefully") This spell is for when you want to quit
  Vim _without saving any changes you made_ since the last time you saved. Be
  careful with this one, as it will throw away unsaved work!
  - Type **`:`**
  - Then type **`q!`**
  - Then press **`Enter`**

  You might use this if you made a lot of mistakes and just want to start over
  from the last saved version.

## Putting it Together: Practice Time

1. Open a text file with Vim (`vim practice.txt`).
2. Add some new words (by pressing `i` to enter Insert Mode, typing, then
   `Escape` to go back to Normal Mode).
3. Now, try to quit without saving:
   - Press **`:`**
   - Type **`q`**
   - Press **`Enter`**
   - Vim will probably stop you and say `No write since last change`.
4. Now, save your changes:
   - Press **`:`**
   - Type **`w`**
   - Press **`Enter`**
5. Now that you've saved, you can quit:
   - Press **`:`**
   - Type **`q`**
   - Press **`Enter`**
6. Open the file again (`vim practice.txt`). You should see all your saved
   changes!
7. Make some new changes, but this time, save and quit all at once:
   - Press **`:`**
   - Type **`wq`**
   - Press **`Enter`**

Fantastic! You've learned the most important basic spells for using Vim. You can
now open files, move around, make changes, save your work, and exit. You're well
on your way to becoming a Vim master!

## Navigation

- Previous:
  [Chapter 05: Vim Basics: Editing Your Code (Insert Mode)](@/ttk/install-vim/05-vim-editing.md)
