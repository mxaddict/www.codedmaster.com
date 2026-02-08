+++
title = "Teach The Kids (aka TTK): Quest App"
description = "Welcome to the 'Teach The Kids' Quest App series! Learn Rust programming fundamentals by building a command-line quest manager step-by-step."
paginate_by = 5
sort_by = "slug"
+++

Welcome, Young Adventurer!

Get ready for an exciting journey into the world of computer programming! You're
about to learn how to build your very own "Quest App" using something called
Rust. Think of it like building with digital LEGOs!

## Getting Started

Follow these steps to get your Rust application up and running:

### Step 1: Get the Code onto Your Computer (Clone the Repository)

Imagine your computer is a magical sketchbook, and this project is a cool
drawing on someone else's sketchbook. To get a copy of that drawing onto _your_
sketchbook, we use a special magic word called `git clone`.

Open your black screen (that's your "terminal" or "command line") and carefully
type this spell, then press the `Enter` key:

```bash
git clone https://github.com/mxaddict/ttk.git
```

This command will magically copy all the project files onto your computer! When
it's done, you'll see a new folder appear with our project's name.

### Step 2: Go Inside Your Project Folder

Now that you have the project copied, let's go inside its special folder. It's
like walking into your secret clubhouse!

Type this command in your terminal and press `Enter`:

```bash
cd ttk
```

This command `cd` means "change directory", and it takes you right into our
project's folder.

### Step 3: Peek Inside the Code with Vim

Your parent has set up a special secret notebook for coding called `vim`! This
is where we'll look at, read, and even change our code.

Let's open our first program file, which is called `src/main.rs`. It's like
opening the first page of a storybook! Type this command in your terminal and
press `Enter`:

```bash
vim src/main.rs
```

You can also peek at another important file called `Cargo.toml`, which tells
Rust how to build our app:

```bash
vim Cargo.toml
```

**Understanding Vim (Your Secret Notebook):**

- When you first open `vim`, it's in **"Reading Mode"** (we call it `normal`
  mode). In this mode, you can read and move around the text without
  accidentally changing anything.
  - To look around, use these keys like a game controller:
    - `h`: move left
    - `l`: move right
    - `j`: move down
    - `k`: move up
- To start **"Writing Mode"** (we call it `insert` mode) and type new words or
  change existing ones, just press the letter `i`. You'll see `-- INSERT --`
  appear at the bottom, letting you know you can type!
- When you're done writing and want to go back to **"Reading Mode"**, just press
  the `Escape` key (it's usually in the top-left corner of your keyboard).
- If you've made changes and want to save your work (like saving a drawing),
  first go back to **"Reading Mode"** (press `Escape`), then type `:w` and press
  `Enter`.
- When you're finished looking at the file and want to close your secret
  notebook, first go back to **"Reading Mode"** (press `Escape`), then type `:q`
  and press `Enter`.

### About This Super Cool Project

This is where your adventure truly begins! This project is a simple computer
program written in Rust. Right now, it's a friendly "Hello, world!" program that
just says hi! You'll find its main magic words in `src/main.rs`, and its
instruction book for Rust in `Cargo.toml`.

Our big goal is to turn this simple program into an amazing **quest command line
app**! You'll be able to use it to:

- **Create** new quests for yourself (like "Learn a new Rust command!").
- **Remove** quests that have been completed.

Imagine having your very own digital quest log! Once we get this first version
working, we'll use it to track all the cool new features we'll add to _your_
quest app! How exciting is that?!
