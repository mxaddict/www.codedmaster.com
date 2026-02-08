+++
date = 2026-02-09
title = "Chapter 05: Quest App: Deleting Your Quests (Removing Items)"
description = "For young learners! Learn how to implement a 'remove' command in your Rust Quest App to delete completed or unwanted quests from your list and persist the changes to the file."
[taxonomies]
tags = ["rust", "programming", "tutorial", "cli", "quest app", "education", "kids", "children", "young", "learners"]
+++

Great job on saving your quests! But what if you finish a quest, or decide you
don't want to do it anymore? We need a way to remove quests from our list!

## Introducing the `remove` Command

We'll add a new command to our app. You'll be able to tell your Quest App to
`remove` a quest by its number. For example, if you want to remove the 2nd quest
in your list, you would type:

```bash
cargo run remove 2
```

This means we need to get a little smarter with how our app understands your
commands!

## Updating Your `main.rs` for Removal

Here's how we'll change our `main.rs` to handle removing quests. This will be
the most complex update yet, but you're a super programmer now, so you can do
it!

```rust
use std::fs;     // For reading and writing files
use std::io::Write; // For writing to files

fn main() {
  // --- Step 1: Load Quests from quests.txt (Same as before) ---
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
      let _ = fs::File::create("quests.txt").expect("Could not create quests.txt!");
    }
  }

  // --- Step 2: Handle Command-Line Arguments (NEW LOGIC HERE!) ---
  let args: Vec<String> = std::env::args().collect();

  // Check if there's a command like "remove" or "add"
  if args.len() > 1 {
    let command = &args[1]; // The first word after 'cargo run' is our command

    match command.as_str() {
      "add" => { // If the command is "add" (optional, but good to be clear)
        let new_quest_description = args[2..].join(" ");
        if !new_quest_description.is_empty() {
          quests.push(new_quest_description.clone());
          println!("Awesome! We added your new quest: {}", new_quest_description);
          // We will save all quests later, after potential removals
        } else {
          println!("To add a new quest, type 'cargo run add <your quest>'.");
        }
      },
      "remove" => { // If the command is "remove"
        if args.len() > 2 {
          // Try to get the quest number you want to remove
          let index_str = &args[2];
          if let Ok(index_num) = index_str.parse::<usize>() {
            // Remember: lists in programming start counting from 0, not 1!
            // So, if you say "remove 2", we remove the item at index 1.
            let actual_index = index_num - 1;

            if actual_index < quests.len() {
              let removed_quest = quests.remove(actual_index);
              println!("Quest removed: "{}"", removed_quest);
            } else {
              println!("Oops! There is no quest number {} to remove.", index_num);
            }
          } else {
            println!("Please provide a valid number for the quest to remove.");
          }
        } else {
          println!("To remove a quest, type 'cargo run remove <quest_number>'.");
        }
      },
      _ => {
        // If it's not "add" or "remove", treat it as adding a quest for simplicity
        let new_quest_description = args[1..].join(" ");
        if !new_quest_description.is_empty() {
          quests.push(new_quest_description.clone());
          println!("Awesome! We added your new quest: {}", new_quest_description);
        }
      }
    }
  } else {
    println!("Type 'cargo run add <your quest>' to add a quest.");
    println!("Type 'cargo run remove <quest_number>' to remove a quest.");
  }

  // --- Step 3: Save ALL Quests Back to File (NEW LOGIC HERE!) ---
  // After we've possibly added or removed quests, we need to save the *entire*
  // updated list back to quests.txt. We can't just append anymore for removals!
  let quests_to_save: Vec<String> = quests.iter()
    .map(|q| format!("{}
", q))
    .collect();
  let all_quests_content = quests_to_save.join(""); // Join all lines together

  fs::write("quests.txt", all_quests_content)
    .expect("Could not write quests to file!");


  // --- Step 4: Display All Quests (Same as before) ---
  println!("
--- Your Current Quests ---");
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

## What's New and Exciting Here?

1. **More Clever Argument Handling:**
   - `let command = &args[1];` We now look at the _second_ word you type (after
     `cargo run`) to see if it's a special `command` like "add" or "remove".
   - `match command.as_str() { ... }`: This is a powerful Rust tool that lets us
     easily check what `command` you typed and do different things for each.
   - **"add" Command:** We made an explicit "add" command now. If you just type
     `cargo run <your quest>`, it will still work, but
     `cargo run add <your quest>` is clearer.
   - **"remove" Command:**
     - `let index_str = &args[2];` We grab the third word, which should be the
       _number_ of the quest to remove.
     - `if let Ok(index_num) = index_str.parse::<usize>()`: We try to turn the
       text (like "2") into a real number (`usize`). `usize` is a type of number
       Rust uses for counting list items. `Ok` means it worked!
     - `let actual_index = index_num - 1;`: This is important! In programming,
       lists usually start counting from 0 (0, 1, 2...) not 1 (1, 2, 3...). So
       if you say "remove 2", it's actually the item at position 1 in Rust's
       list.
     - `quests.remove(actual_index);`: This is the magic line that takes the
       quest out of our `quests` list!
     - We added checks to make sure you give a valid number, so the app doesn't
       crash if you make a mistake!

2. **Rewriting the Entire File for Saving:** _Before, we used `.append(true)` to
   just add a new line. But if we remove a quest from the \_middle_ of the list,
   simply appending won't fix the file._Instead, after we've made all our
   changes (added or removed quests), we gather \_all_ the quests from our
   `quests` list again. _
   `let quests_to_save: Vec<String> = quests.iter().map(|q| format!("{} ", q)).collect();`
   This line goes through every quest in our list, adds a new line character
   (` `) to the end of each, and collects them into a new list._
   `let all_quests_content = quests_to_save.join("");` This combines all those
   quest-with-newline strings into one giant string. *
   `fs::write("quests.txt", all_quests_content).expect(...)`: This is the new
   way to save! `fs::write` completely*replaces\* the content of `quests.txt`
   with our `all_quests_content`. This means `quests.txt` will always perfectly
   match our `quests` list in the program!

## Your Turn

1. **Update your `src/main.rs` file** with the complete code example from above.
2. **Make sure your `quests.txt` file has some quests in it** (from previous
   steps).
3. **Run your program to see your quests:**

   ```bash
   cargo run
   ```

   (You should see your current list.)

4. **Add a new quest:**

   ```bash
   cargo run add learn more Rust
   ```

   (Then run `cargo run` again to see it in the list.)

5. **Now, remove a quest!** Look at your `cargo run` output, find the number of
   a quest you want to remove (e.g., if "Learn more Rust" is number 4):

   ```bash
   cargo run remove 4
   ```

   (Run `cargo run` again to see the updated list, and check your `quests.txt`
   file too!)

You now have a Quest App that can add and remove quests, and it remembers
everything in your `quests.txt` file! This is a huge milestone! You're becoming
a true programmer!

## Navigation

- Previous:
  [Quest App: Making Quests Permanent (Saving to a File)](@/ttk/04-saving-quest-to-the-quests-file.md)
