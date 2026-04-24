+++
date = 2026-04-24
title = "Introducing SQEEL: A Fast, Vim-Native SQL Client in Rust"
description = "SQEEL is a blazing-fast SQL client written in Rust — vim bindings first, no Electron, no JVM. Terminal UI and native GUI, MySQL/Postgres/SQLite support, and LSP-powered completions."
[taxonomies]
tags = ["rust", "cli", "sql", "vim", "tui", "gui", "database", "open source", "sqeel"]
+++

Every SQL client I tried eventually annoyed me. DBeaver hauls a JVM. TablePlus
is closed-source. The Electron crowd burns 500MB of RAM to show a grid. I wanted
something that starts instantly, lives in the terminal, and respects my muscle
memory. So I built one.

Meet **SQEEL**.

## What is SQEEL? ⚡

[SQEEL](https://github.com/sqeel-sql/sqeel) is a fast, vim-native SQL client
written in Rust. No Electron. No JVM. It ships two binaries from one workspace:

- `sqeel` — a terminal UI built on ratatui
- `sqeel-gui` — a native GUI built on iced

Same core, same keybindings, same config. Pick the one your mood wants today.

## Features

- **Native Rust** — instant startup, single binary
- **Vim bindings** first class, not an afterthought
- **Mouse support** in every pane (even in the TUI)
- **MySQL, PostgreSQL, SQLite** via `sqlx`
- **tree-sitter** SQL syntax highlighting, dialect-aware
- **LSP integration** with [`sqls`](https://github.com/sqls-server/sqls) for
  completions and inline diagnostic underlines
- **Schema browser** — click or `hjkl` to expand/collapse
- **Editor tabs** with lazy loading and 5-minute RAM eviction
- **Auto-save** SQL buffers, result history, query history
- **tmux-aware** pane navigation — `Ctrl+HJKL` crosses tmux panes cleanly
- **Vim status bar** and command mode (`:q`, `:w`, all the muscle memory)

## Layout

```
┌──────────┬─────────────────────────────┐
│          │  [tab1] [tab2]              │
│  Schema  │         Editor              │
│  (15%)   │         (85%)               │
│          │                             │
│          ├─────────────────────────────┤
│          │         Results             │
│          │      (shows on query)       │
└──────────┴─────────────────────────────┘
```

Results hide when empty so the editor fills the right pane. Run a query and the
results pane expands to 50%. Dismiss with `q` and you're back to full-size
editing. No wasted pixels.

## Connections as Files

Every connection is one TOML file in `~/.config/sqeel/conns/`. Filename becomes
the display name.

```toml
# ~/.config/sqeel/conns/prod.toml
url = "postgres://user:pass@host/db"
```

```toml
# ~/.config/sqeel/conns/local.toml
url = "mysql://localhost/mydb"
```

Drop a file in, it shows up in the connection switcher (`<leader>c`). Version
control it, symlink it, rsync it between machines. No proprietary blob.

## The Vim Bit

If you already live in vim, you already know how to drive SQEEL. `i` to insert,
`Esc` to normal, `v` for visual, `:` for command mode, `/` to search. Leader key
(default `Space`) opens the fun stuff:

| Key                | Action               |
| ------------------ | -------------------- |
| `<leader>c`        | Connection switcher  |
| `<leader>n`        | New scratch tab      |
| `<leader>r`        | Rename current tab   |
| `<leader>d`        | Delete tab (confirm) |
| `<leader><leader>` | Fuzzy file picker    |

Running a query is `Ctrl+Enter` for the statement under the cursor, or
`Ctrl+Shift+Enter` to run every statement in the buffer.

## LSP-Powered Autocomplete

Point `editor.lsp_binary` at [`sqls`](https://github.com/sqls-server/sqls) and
you get schema-aware completions, hover docs, and inline diagnostic underlines —
the same machinery your editor already uses, wired into the SQL editor pane. No
bespoke completion engine to maintain, no magic.

## Two UIs, One Core

The workspace splits cleanly:

```
sqeel-core/   # state, DB, query runner, schema, config
sqeel-tui/    # ratatui terminal provider
sqeel-gui/    # iced native GUI provider
sqeel/        # binaries: sqeel + sqeel-gui
```

All the logic — connections, schema, query execution, history, eviction — lives
in `sqeel-core`. The TUI and GUI are thin providers that render the same state.
Fix a bug in the core, both UIs benefit. Want a web provider next? Drop in
another crate.

## Why Rust?

Same reasons as always: performance, single-binary distribution, and `sqlx`.
SQEEL opens instantly, connects to a real production database without a JVM
warming up, and fits in a `cargo install` one-liner. No runtime to manage, no
package manager to fight.

## How to Get It 📦

```bash
cargo install --git https://github.com/sqeel-sql/sqeel --bin sqeel
cargo install --git https://github.com/sqeel-sql/sqeel --bin sqeel-gui
```

Or clone and build:

```bash
git clone https://github.com/sqeel-sql/sqeel
cd sqeel
cargo build --release
```

Binaries land in `target/release/sqeel` and `target/release/sqeel-gui`.

## Final Thoughts

SQEEL started the way most of my tools do — I was annoyed at something, and a
weekend later there was a prototype. It's now my daily driver for every database
I touch. If you live in vim, write a lot of SQL, and resent every Electron SQL
client you've ever opened, give it a spin. Issues and PRs welcome at
[github.com/sqeel-sql/sqeel](https://github.com/sqeel-sql/sqeel). 🍻
