+++
date = 2026-02-09
title = "Chapter 01: Quest App: Showing Your Progress (Output)"
description = "For young learners! Learn how to make your Rust program display text on the screen using `println!` and store multiple quests using `Vec` (Vector) for your Quest App."
[taxonomies]
tags = ["rust", "programming", "tutorial", "cli", "quest app", "education", "kids", "children", "young", "learners"]
+++

Hey there, Young Coder!

You've started your very own Rust project and explored its first bits of code.
Now, let's learn how to make your Rust program _talk back to you_! This is super
important for our Quest App so it can show you your quests.

## Making Your Program Talk: `println!`

In Rust, the easiest way to make your program display text on the screen (your
terminal) is by using a special command called `println!`. It's like your
program saying something out loud!

Here's how it works:

```rust
fn main() {
  // This will print "Hello, Quest Master!"
  println!("Hello, Quest Master!");

  // This will print another message
  println!("Are you ready for an adventure?");
}
```

When you run this code, you'll see both sentences appear on separate lines in
your terminal. The `!` at the end of `println` means it's a "macro", which is a
bit like a super-powered function in Rust.

## Storing Your Quests: The `Vec` (Vector)

For our Quest App, we need a way to store multiple quests. Imagine a list where
you write down all your tasks. In Rust, we have something similar called a `Vec`
(pronounced "veck", short for Vector). It's a growable list where you can keep
many things, like our quest descriptions!

Let's make a `Vec` to hold a couple of sample quests:

```rust
fn main() {
    // Create an empty list (Vec) where we'll store our quests.
    // We tell Rust it will hold words (Strings).
    let mut quests: Vec<String> = Vec::new();

    // Add our first quest to the list
    quests.push(String::from("Explore the mysterious forest"));

    // Add another quest to the list
    quests.push(String::from("Learn a new Rust command"));

    // Now, let's make our program tell us what quests we have!
    println!("--- Your Current Quests ---");

    // This special loop will go through each quest in our 'quests' list
    for quest in quests {
        println!("- {}", quest); // And print each one!
    }

    println!("---------------------------");
}
```

## What's Happening Here?

1. `let mut quests: Vec<String> = Vec::new();`
   - `let mut` means we're creating a new variable named `quests` that _can be
     changed_ (`mut` for mutable).
   - `Vec<String>` tells Rust that `quests` will be a list (`Vec`) containing
     text (`String`).
   - `Vec::new()` creates an empty list for us to start with.

2. `quests.push(String::from("..."));`
   - The `.push()` command is how we add new items to our `quests` list.
   - `String::from("...")` turns our simple text into a `String` that can be
     stored in our `Vec`.

3. `for quest in quests { ... }`
   - This is a `for` loop! It's a way to do something for _each_ item in a list.
   - For every `quest` (which is what we call each item temporarily) in our
     `quests` list, it will run the code inside the `{}`.

4. `println!("- {}", quest);`
   - Inside the loop, `println!` is used again.
   - The `{}` is a special placeholder. Rust will replace `{}` with the value of
     the `quest` variable for each item in the list. So, it will print "-
     Explore the mysterious forest", then "- Learn a new Rust command".

## Your Turn

Try changing your `src/main.rs` file to match the code above.

Then, run your program from the terminal:

```bash
cargo run
```

You should see your program list out your two quests! This is a super important
step for building our Quest App, as it lets you see all the quests you have to
do! Great job!

## Navigation

- Previous:
  [Chapter 00: Starting Your Rust Quest Project](@/ttk/quest-app/00-starting-the-project.md)
- Next:
  [Chapter 02: Quest App: Reading Your Commands (Input)](@/ttk/quest-app/02-reading-input.md)
