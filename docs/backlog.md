# Backlog

## kryptic-sh projects without an article

Checked against `gh repo list kryptic-sh` on 2026-09-15. Only `sqeel` and `infr`
have posts. Remaining projects, roughly in order of how ready they are to write
about (release tag at time of checking in brackets). Read the repo's README,
CHANGELOG and `docs/` before writing; READMEs and results docs have disagreed
before (infr's README and `docs/perf/results.md` count benchmark wins
differently: strictly faster versus faster-or-tied).

- **buffr** (v0.14.16): Vim-modal web browser on Chromium Embedded Framework,
  Wayland-only on Linux, releases for Linux/macOS/Windows. Most-starred after
  infr; strong standalone article.
- **hrdr** (v0.15.3): agentic coding harness for any OpenAI-compatible endpoint
  (infr, llama.cpp, OpenRouter). Pairs naturally with the infr and opencode
  posts.
- **hjkl** (v0.41.6): the Vim engine, rope buffer and modal primitives extracted
  from sqeel, shared by sqeel, buffr, inbx and others, plus a standalone `hjkl`
  editor. Good "how the stack fits together" post.
- **krypt** (v0.2.2): copy-based cross-platform dotfiles manager that replaces
  GNU Stow. Once written, the dotfiles posts ("How to Setup a Dotfiles Repo", "A
  Deep Dive Into My Dotfiles", the Stow sections of the CLI stack post) should
  get an editor's note pointing to it.
- **pikr** (v0.8.13): Vim-modal launcher/picker replacing rofi. The two autofill
  posts use rofi, so they should link to it as the modern alternative.
- **gpur** (v0.13.2): btop-style GPU monitor TUI for NVIDIA, AMD, Intel and
  Apple; README says beta, only the AMD Linux path is exercised on real
  hardware.
- **inbx** (v0.5.0 release, Cargo.toml at 0.7.0): modal Vim email client, CLI
  and TUI.
- **hodl** (v0.7.1): multi-chain TUI light wallet that includes Navio; can link
  from the Navio mainnet post.
- **crcbl** (no release): "Crucible", cross-platform GPU game engine (Vulkan,
  Metal, D3D12, WebGPU) with its own windowing; demos at crcbl.kryptic.sh.
- **wayr** (no release): Wayland-only windowing toolkit used by buffr and pikr.
  Probably best covered inside the buffr or pikr article rather than alone.
- **langr** (no release): language detector that reuses an LLM tokenizer
  vocabulary with a trained token-to-language table, no neural net at runtime.
- **tikr** (no release, pre-alpha): market-making engine. README carries a
  financial-risk warning; any article must repeat it prominently.
- **lyr** (no release): Wayland status bar; README is two lines ("Work in
  progress"). Not ready for an article.

Not articles: `homebrew-tap`, `scoop-bucket`, `.github` and
`kryptic-sh.github.io` are packaging and org infrastructure.

## Content ideas not acted on

- **SQEEL post** links to `github.com/sqeel-sql/sqeel`. That now redirects to
  `github.com/kryptic-sh/sqeel`; update the links to the canonical URL.

- **"Top Terminals for Fast, Keyboard-Driven Development"** only covers
  Alacritty, though the title promises several terminals. Either retitle it or
  add short sections on others (WezTerm, Kitty, Ghostty, foot).
- **"My Journey into Local AI Coding"** never says what hardware runs
  `qwen3-coder:30b`, and suggests a "modest home computer" will do. A 30B model
  needs roughly 20GB+ of VRAM or unified memory, so naming the actual machine
  would make the post more useful and more accurate.
- **Dotfiles posts** describe `.menu-autofill` bound in `hyprland.conf`. The
  live dotfiles have since moved to `krypt menu autofill` bound in
  `hyprland.lua` (other scripts the posts mention were not re-checked). The
  posts were left as dated snapshots on purpose; an editor's note or follow-up
  post could point readers at the current setup.
- **Quest App chapters** mix 2-space and 4-space indentation in Rust code blocks
  (rustfmt uses 4). Every chapter compiles without warnings, so this was left
  alone.
