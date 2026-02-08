+++
date = 2026-02-09
title = "Chapter 02: Quest App: Reading Your Commands (Input)"
description = "For young learners! Learn how your Rust Quest App can read command-line arguments to accept new quest ideas from the user, making your program interactive."
[taxonomies]
tags = ["rust", "programming", "tutorial", "cli", "quest app", "education", "kids", "children", "young", "learners"]
+++

Hello, Future Quest Master!

Now that you know how to get your Rust project and peek at its code, let's learn
how to tell your `quest` app what to do! When you type commands into the
terminal, you can also give your program extra information. These are called
"arguments."

Imagine you want to create a new quest. You'd want to tell your `quest` app
_what_ the quest is, right? Like:

```bash
cargo run learn about Rust
```

In this command:

- `cargo run` is how we tell Rust to build and run our program.
- `learn about Rust` is the extra information, or "arguments", we're giving to
  our `quest` app. We want this to become our new quest!

## How Rust Reads Your Words

Rust has a special way to listen for these arguments you type. We use something
called `std::env::args()`. Don't worry too much about the big words right now,
just know it's like a magical ear for your program!

Here's how we can make our `main.rs` file listen for your quest description and
add it to our list of quests:

```rust
fn main() {
    // Collect all the arguments you typed into a list
    let args: Vec<String> = std::env::args().collect();

    // The first argument is always the name of our program.
    // If there are arguments after the program name, it means you're
    // trying to create a new quest!
    let mut new_quest_description: Option<String> = None;
    if args.len() > 1 {
        // We join all the quest words together with spaces to make our quest description.
        new_quest_description = Some(args[1..].join(" "));
    }

    // Start with some quests we already know about (just like in 01-displaying-output.md!)
    let mut quests: Vec<String> = Vec::new();
    quests.push(String::from("Explore the mysterious forest"));
    quests.push(String::from("Learn a new Rust command"));

    // If you provided a new quest, let's add it to our list!
    if let Some(quest_text) = new_quest_description {
        quests.push(quest_text);
        println!("Awesome! We added your new quest.");
    } else {
        println!("To add a new quest, type 'cargo run' followed by your quest, like:");
        println!("  cargo run find the golden apple");
    }

    // Now, let's make our program tell us what quests we have,
    // including any new ones!
    println!("");
    println!("--- Your Current Quests ---");

    for quest in quests {
        println!("- {}", quest);
    }

    println!("---------------------------");
}
```

## What's Happening Here Now?

Let's look at the new magic we added:

1. `let mut new_quest_description: Option<String> = None;`
   - We created a special variable `new_quest_description`. It uses
     `Option<String>`, which is Rust's way of saying "this might have some text
     (`String`), or it might have nothing (`None`)". We start it with `None`
     because we don't know yet if you've given us a new quest.

2. `if args.len() > 1 { ... }`
   - This is how we check if you actually typed something after `cargo run`.
     Remember, `args[0]` is always the program name. So if `args.len()` (the
     number of items in `args`) is greater than 1, it means you gave us more
     words for a new quest!
   - `new_quest_description = Some(args[1..].join(" "));` If you did give us
     words, we put them into our `new_quest_description` inside `Some()`.

3. `let mut quests: Vec<String> = Vec::new();`
   - Just like in `01-displaying-output.md`, we start our list of `quests`. We
     even added the same two starting quests to it!

4. `if let Some(quest_text) = new_quest_description { ... }`
   - This is a clever way to say: "If `new_quest_description` actually has some
     text inside (`Some(quest_text)`), then let's take that text (which we'll
     call `quest_text` for a moment) and do something with it."
   - `quests.push(quest_text);` If there was a new quest from your command, we
     add it to our `quests` list!
   - The `else` part tells you how to add a new quest if you didn't provide one
     this time.

5. The final `println!` loop:
   - This is the same as in `01-displaying-output.md`! It goes through our
     `quests` list (which now might include your new quest!) and prints each one
     out.

Now your Quest App can both _read_ new quest ideas and _show_ you all your
quests! Fantastic progress!

## Your Turn

Now for the fun part!

1. **Update your `src/main.rs` file** with the new code from above.
2. **Run it without any extra words:**

   ```bash
   cargo run
   ```

   You should see your two default quests and a message telling you how to add a
   new one.

3. **Run it with a new quest idea:**

   ```bash
   cargo run find the golden apple
   ```

   You should see all three quests (the two old ones, plus your new "find the
   golden apple" quest)! Try it with different quest ideas!

You're doing great! You've just combined input (reading your command) and output
(showing your quests)!

## Navigation

- Previous:
  [Chapter 01: Quest App: Showing Your Progress (Output)](@/ttk/quest-app/01-displaying-output.md)
- Next:
  [Chapter 03: Quest App: Saving and Loading Your Adventures (Reading from a File)](@/ttk/quest-app/03-reading-quests-from-a-file.md)
