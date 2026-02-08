+++
date = 2026-02-09
title = "Quest App: Saving and Loading Your Adventures (Reading from a File)"
description = "Discover how to persist your Quest App's data by learning to save and load quests from a `quests.txt` file in Rust, ensuring your progress is never lost."
[taxonomies]
tags = ["rust", "programming", "tutorial", "cli", "quest app", "education"]
+++

Hi there, Super Programmer!

You've done an amazing job so far! Your Quest App can now take new quests from
your commands and show you a list of quests. But there's a tiny problem: every
time you close the program, all your quests disappear! That's not very helpful,
is it?

Let's fix that by learning how to **save your quests to a file** and **load them
back** when your program starts! This way, your quests will always be there,
just like notes in a magical notebook.

## Our Quest File: `quests.txt`

We're going to create a simple text file named `quests.txt`. Each line in this
file will be one of your quests.

**Before you continue, create a new file named `quests.txt` in your project
folder (next to `src` and `Cargo.toml`).**

Inside `quests.txt`, you can write quests like this:

```txt
Explore the mysterious forest
Learn a new Rust command
Find the hidden treasure
Bake a delicious cake
```

## How Rust Reads Your File

Rust has special tools to read files from your computer. We'll use
`std::fs::read_to_string` to read the entire file, and then we'll split it into
individual quests.

Here's how we can update our `main.rs` to load quests from `quests.txt`:

```rust
use std::fs; // We need to 'use' the filesystem tools!

fn main() {
    // --- Part 1: Load Quests from quests.txt ---
    let mut quests: Vec<String> = Vec::new();

    // Try to read the quests.txt file
    let quests_file_content = fs::read_to_string("quests.txt");

    match quests_file_content {
        Ok(content) => {
            // If the file was read successfully, split the content by lines
            // and add each line as a quest.
            for line in content.lines() {
                if !line.trim().is_empty() { // Make sure we don't add empty lines
                    quests.push(line.to_string());
                }
            }
            println!("Loaded {} quests from quests.txt!", quests.len());
        },
        Err(error) => {
            // If there was an error (like the file not existing),
            // we'll just say so and start with an empty quest list.
            println!("Could not read quests.txt: {}", error);
            println!("Starting with an empty quest list. Make sure quests.txt exists!");
        }
    }

    // --- Part 2: (Optional) Add a New Quest from Command-Line Arguments ---
    let args: Vec<String> = std::env::args().collect();
    let mut new_quest_description: Option<String> = None;
    if args.len() > 1 {
        new_quest_description = Some(args[1..].join(" "));
    }

    if let Some(quest_text) = new_quest_description {
        quests.push(quest_text);
        println!("Awesome! We added your new quest.");
        // TODO: In the future, we should also save this new quest to the file!
    } else {
        println!("To add a new quest, type 'cargo run' followed by your quest, like:");
        println!("  cargo run find the golden apple");
    }


    // --- Part 3: Display All Quests ---
    println!("");
    println!("--- Your Current Quests ---");
    if quests.is_empty() {
        println!("No quests found! Time to add some new adventures!");
    } else {
        for (index, quest) in quests.iter().enumerate() {
            println!("{}. {}", index + 1, quest);
        }
    }
    println!("---------------------------");
}
```

## What's New Here?

1. `use std::fs;`
   - This line tells Rust that we want to use the tools for working with the
     "filesystem" (files and folders).

2. `let quests_file_content = fs::read_to_string("quests.txt");`
   - This is the magical line that tries to read the entire `quests.txt` file
     and puts its contents into `quests_file_content`.
   - `read_to_string` doesn't just give us the content; it gives us a `Result`!
     This `Result` can be `Ok(content)` (meaning it worked, and `content` has
     the text) or `Err(error)` (meaning something went wrong, and `error` tells
     us what).

3. `match quests_file_content { Ok(content) => { ... }, Err(error) => { ... } }`
   - The `match` statement is like a super-smart `if/else` that handles the
     `Result`.
   - If `Ok(content)`, we take the `content` (the text from the file).
   - `for line in content.lines() { ... }` We then go through each `line` in the
     file content.
   - `if !line.trim().is_empty()` This checks if the line isn't just empty
     spaces before adding it.
   - `quests.push(line.to_string());` And finally, we add each valid line as a
     quest to our `quests` list.
   - If `Err(error)`, we print a friendly message telling us what went wrong.

4. **Combining with Previous Lessons:** Notice how we've put together everything
   we learned!
   - We first load quests from the file.
   - Then, we check if you gave us a _new_ quest using command-line arguments.
   - Finally, we print out _all_ the quests, both loaded from the file and any
     new one you added!

5. `println!("{}. {}", index + 1, quest);`
   - We've added `enumerate()` to our loop to give each quest a number, making
     our list look even better!

## Your Turn

1. **First, create a `quests.txt` file** in your main project folder and add a
   few quests to it (one per line).
2. **Update your `src/main.rs` file** with the full code example provided above.
3. **Run your program:**

   ```bash
   cargo run
   ```

   You should see all the quests from your `quests.txt` file printed out!

4. **Try adding a new quest:**

   ```bash
   cargo run defeat the evil wizard
   ```

   You'll see your `quests.txt` quests _plus_ your new quest! (Even though it
   won't save to the file yet, we'll get to that later!)

You're building a real app now! Keep up the amazing work!
