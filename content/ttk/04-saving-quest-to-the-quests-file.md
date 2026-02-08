+++
date = 2026-02-09
title = "Quest App: Making Quests Permanent (Saving to a File)"
description = "For young learners! Make your Quest App quests permanent by learning to save newly added quests to a `quests.txt` file in Rust, ensuring your progress is always up-to-date."
[taxonomies]
tags = ["rust", "programming", "tutorial", "cli", "quest app", "education", "kids", "children", "young", "learners"]
+++

Fantastic work, Adventurer!

Your Quest App can now read quests from a file and even add new ones from your
commands. But there's still one tiny step missing: when you add a _new_ quest
using `cargo run`, it doesn't stay in `quests.txt` when you close the program.
Let's fix that so your quest log is always up-to-date!

## The Magic of Writing to a File

To make our new quests permanent, we need to write them into our `quests.txt`
file. We'll use some special tools in Rust that let us open the file and add new
lines to it.

Here's how we'll update our `main.rs` file to save new quests:

```rust
use std::fs;        // For reading and writing files
use std::io::Write; // We need this to use the 'write_all' function

fn main() {
  // --- Part 1: Load Quests from quests.txt ---
  let mut quests: Vec<String> = Vec::new();

  let quests_file_content = fs::read_to_string("quests.txt");

  match quests_file_content {
    Ok(content) => {
      for line in content.lines() {
        if !line.trim().is_empty() {
          quests.push(line.to_string());
        }
      }
      println!("Loaded {} quests from quests.txt!", quests.len());
    },
    Err(error) => {
      println!("Could not read quests.txt: {}", error);
      println!("Starting with an empty quest list. Make sure quests.txt exists!");
      // We'll create the file if it doesn't exist
      // to avoid future errors when writing
      let _ = fs::File::create("quests.txt").expect("Could not create quests.txt!");
    }
  }

  // --- Part 2: (Optional) Add a New Quest from Command-Line Arguments ---
  let args: Vec<String> = std::env::args().collect();
  let mut new_quest_description: Option<String> = None;
  if args.len() > 1 {
    new_quest_description = Some(args[1..].join(" "));
  }

  if let Some(quest_text) = new_quest_description {
    // Add the new quest to our list in memory
    // We use .clone() because we need quest_text twice
    quests.push(quest_text.clone());

    // --- NEW PART: Save the new quest to the quests.txt file! ---
    let mut file = fs::OpenOptions::new()
      // This means "add to the end of the file"
      .append(true)
      // This means "create the file if it doesn't exist"
      .create(true)
      // Try to open our quest file
      .open("quests.txt")
      // If it fails, stop and tell us why
      .expect("Could not open quests.txt for writing!");

    // Write the new quest followed by a new line character
    if let Err(e) = writeln!(file, "{}", quest_text) {
      eprintln!("Couldn't write to file: {}", e);
    }

    println!("Awesome! We added your new quest and saved it!");
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

## What's Changed and New Here?

1. `use std::io::Write;`
   - We added this new `use` line because the `writeln!` function we're using
     comes from this part of Rust's tools.

2. `let _ = fs::File::create("quests.txt").expect("Could not create quests.txt!");`
   - In the `Err` part when loading quests, we added this line. If `quests.txt`
     doesn't exist, this will create an empty one so we can write to it later
     without problems. The `let _ =` means we don't care about the result, we
     just want it to happen.

3. `quests.push(quest_text.clone());`
   - You might notice `.clone()` here. Because we're using `quest_text` to add
     to our `quests` list _and_ to write to the file, Rust needs two separate
     copies of it. `clone()` makes a copy!

4. `let mut file = fs::OpenOptions::new()...`
   - This is the super important new part for saving!
   - `fs::OpenOptions::new()`: We're telling Rust we want to open a file with
     some special rules.
   - `.append(true)`: This is the key! It means "don't erase the file, just add
     new stuff to the very end."
   - `.create(true)`: This means "if `quests.txt` doesn't exist yet, please make
     it for me!"
   - `.open("quests.txt")`: Finally, try to open the file with these rules.
   - `.expect(...)`: If anything goes wrong (like your computer doesn't let us
     open the file), this will stop the program and show our message.

5. `if let Err(e) = writeln!(file, "{}", quest_text) { ... }`
   - `writeln!(file, "{}", quest_text)`: This is like `println!`, but instead of
     printing to the screen, it `write`s the `quest_text` to our `file`
     variable, and then adds a new line (`ln!`) at the end.
   - `if let Err(e) = ...`: Just like when we read the file, writing can
     sometimes have errors. This checks if there was an `Err`or `e` and prints
     it if something went wrong while writing.

Now, whenever you add a new quest using `cargo run`, it will be added to your
`quests.txt` file permanently!

## Your Turn

1. **Update your `src/main.rs` file** with the complete code example from above.
2. **Make sure your `quests.txt` file exists** (even if it's empty).
3. **Run your program with a new quest:**

   ```bash
   cargo run defeat the evil robot
   ```

   You should see the message "Awesome! We added your new quest and saved it!".

4. **Run your program again, but without adding a new quest:**

   ```bash
   cargo run
   ```

   **MAGIC!** You should now see "defeat the evil robot" in your list of quests,
   even though you didn't type it this time! It was loaded from `quests.txt`!

You've just built a basic system for saving and loading data! That's a huge step
in programming! Keep up the incredible work!

## Navigation

- Previous:
  [Quest App: Saving and Loading Your Adventures (Reading from a File)](@/ttk/03-reading-quests-from-a-file.md)
- Next:
  [Quest App: Deleting Your Quests (Removing Items)](@/ttk/05-removing-quests.md)
