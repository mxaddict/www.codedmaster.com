+++
date = 2026-09-15
title = "Introducing infr: A Pure-Rust, Vulkan-First LLM Inference Engine"
description = "infr is a from-the-metal LLM inference engine written in Rust. It runs Llama, Qwen, Gemma and more on any Vulkan GPU, has native Metal and CPU backends, speaks the OpenAI API, and holds its own against llama.cpp."
[taxonomies]
tags = ["rust", "ai", "local-ai", "llm", "vulkan", "gpu", "inference", "open source", "infr"]
+++

Back in March, I wrote about
[my journey into local AI coding](@/blog/2026-03-11-my-journey-into-local-ai-coding.md)
with Ollama and `qwen3-coder:30b`. That setup worked, but it left me with an
itch I couldn't stop scratching: what is actually happening between my prompt
and my GPU, and how fast could it go if I wrote every layer myself?

So I built one. Meet **infr**.

## What is infr?

[infr](https://github.com/kryptic-sh/infr) is a pure-Rust LLM inference engine
that is **Vulkan-first**, built to run on any mainstream GPU. The only parts
that aren't Rust are the GPU driver calls (Vulkan through the `ash` crate,
called via thin Rust FFI) and the compute shaders themselves (GLSL compiled to
SPIR-V, plus MSL for Apple).

The goal is a from-the-metal inference server where the model and server code
never know which GPU API is running underneath. Three backends sit behind one
`Backend` trait:

- **Vulkan** for AMD, NVIDIA and Intel GPUs, including integrated graphics.
- **Metal** for Apple Silicon, written natively rather than through a
  translation layer.
- **CPU**, a reference implementation that every GPU path is tested against.

I started the repository on June 26, 2026, and it has grown fast: over 1,500
commits and around 175,000 lines of Rust, with a handful of contributors joining
along the way.

## Using It

The CLI is intentionally small:

```bash
infr pull   <model-ref>        # download a model
infr run    <model-ref> [msg]  # chat in the terminal (pulls automatically)
infr serve  <model-ref>        # OpenAI-compatible HTTP API
infr bench / infr compare      # benchmarks, including against llama.cpp
```

Model references work just like llama.cpp's `-hf` flag: `org/repo[:quant]`, with
`Q4_K_M` as the default quant. Even better, infr uses the standard **Hugging
Face Hub cache** (`~/.cache/huggingface/hub`), so a model you already downloaded
with llama.cpp or `huggingface_hub` doesn't get downloaded twice.

```bash
infr run unsloth/Qwen3-1.7B-GGUF:Q4_K_M "What is the capital of France?"
```

## What It Runs

infr loads GGUF files and supports a wide spread of model families:

- **Llama** and **Llama 4** (including Scout's mixture-of-experts)
- **Qwen2 / Qwen2.5**, **Qwen3** (dense and MoE)
- **Qwen3.5 / Qwen3.6**, with their hybrid gated-DeltaNet plus attention layers
- **Gemma 3** and **Gemma 4** (dense, the E2B variant, and the 26B-A4B MoE)
- **DiffusionGemma**, a block text-diffusion model that was the project's
  original target
- **BitNet b1.58**, with ternary weights

Fine-tunes built on any of those backbones run with no code changes. The chat
template is read straight from each GGUF file, so prompts are formatted the way
the model expects.

## Performance: Honest Numbers

I didn't want to write "blazing fast" without receipts, so infr ships its own
benchmarking against llama.cpp (`infr compare`). The
[published results](https://github.com/kryptic-sh/infr/blob/main/docs/perf/results.md)
come from an **AMD Radeon RX 7900 XTX** (24 GB, Vulkan on Mesa RADV), comparing
35 model and quant combinations against a llama.cpp release build, in a snapshot
taken on August 3, 2026.

Here's how often infr came out **faster** than llama.cpp, per benchmark:

| Benchmark                             | infr faster in | Best ratio |
| ------------------------------------- | -------------- | ---------- |
| `pp512` (prompt processing)           | 34 of 35 rows  | 1.43×      |
| `tg128` (token generation)            | 29 of 35 rows  | 1.51×      |
| `tg64@d4096` (generation, 4K context) | 24 of 35 rows  | 1.27×      |
| `pp4@d4096` (short turns, 4K context) | 33 of 35 rows  | 2.19×      |

That last row is the one I care about most. A coding agent sends lots of short
turns on top of a long, growing context, and that is exactly where infr is
strongest.

It isn't a clean sweep, and the results document says so. The losses cluster
around **Qwen3-14B and the larger MoE models**, mostly when generating at depth,
and that is where the remaining work is. Speed also means nothing if the output
is wrong, so correctness is checked separately: tests generate text token for
token on both the GPU and the CPU reference implementation and compare them.

On Apple Silicon, the Metal backend is newer and currently trails llama.cpp's
Metal backend slightly on an M3 Pro, with most rows between 0.8× and 1.0×.

## Two Standout Tricks

### Ternary Models on the GPU

llama.cpp added the **Q2_0** weight type used by Prism ML's Ternary-Bonsai
models (weights trained to just -1, 0 and +1), but only for the CPU. infr runs
them natively on Vulkan, which makes it the only engine that runs these files on
a GPU. On the 7900 XTX, Bonsai-8B generates about **212 tokens per second**. For
context, llama.cpp manages 18.6 on my Ryzen 9 9950X3D, though that is a GPU
against a CPU rather than a like-for-like race.

```bash
infr run prism-ml/Ternary-Bonsai-8B-gguf:Q2_0_g64 "What is the capital of France?"
```

### Models Bigger Than Your VRAM

Llama 4 Scout at `Q2_K` is a 37 GB file, far more than a 24 GB card can hold.
infr's **paged expert cache** keeps recently used experts in VRAM and pages the
rest in as needed. On the 7900 XTX that gives roughly **404 tokens per second**
of prompt processing and **~17 tokens per second** of generation, compared with
136 and 6.55 for llama.cpp's CPU offload.

## Serving: Point Your Tools at It

`infr serve` exposes an OpenAI-compatible HTTP API with streaming:

```bash
infr serve unsloth/Qwen3-14B-GGUF:Q4_K_M   # listens on 127.0.0.1:8080

curl -s localhost:8080/v1/chat/completions -d '{
  "model": "qwen3",
  "messages": [{"role": "user", "content": "What is the capital of France?"}],
  "stream": true
}'
```

It keeps a persistent KV cache across requests, so a follow-up message that
shares a prefix with the previous one doesn't reprocess the whole conversation.
Tool calling uses the model's own chat template, which means it works as a
drop-in backend for OpenAI-API clients like
[opencode](@/blog/2026-04-09-why-opencode-is-my-favorite-cli-coding-agent.md).
It's also the natural backend for [hrdr](https://github.com/kryptic-sh/hrdr),
the agentic coding harness I'm building alongside it.

## Configuration Without Surprises

Every setting (device, context size, sampling, KV cache format, paging budgets,
individual kernel switches) resolves once at startup from four layers, where
later layers win:

```text
defaults  <  config file (TOML)  <  INFR_* environment  <  CLI flags / --set
```

The config file is the first one found out of `--config <path>`, `./infr.toml`,
and `~/.config/infr/config.toml`:

```toml
# ./infr.toml
[device]
ctx = "32k"

[kv]
type_k = "q8_0"
```

Anything without a dedicated flag can still be set from the command line with
`--set`, for example `--set kernels.vulkan.flash_splits=2`.

## Try It Yourself

infr is still an **early work in progress** with no tagged releases yet, so for
now you build it from source. You'll need a Rust toolchain, a working Vulkan
driver, and `glslc` (from the `shaderc` package), which compiles the compute
shaders during the build:

```bash
git clone https://github.com/kryptic-sh/infr.git
cd infr
cargo build --release -p infr-cli
./target/release/infr run unsloth/Qwen3-1.7B-GGUF:Q4_K_M "Hello!"
```

A few things are deliberately parked for now, like MTP speculative decoding (the
reasoning is documented in the repo), and safetensors loading isn't built yet.

## Final Thoughts

infr started as curiosity about what happens under the hood of local AI, and
turned into a deep dive all the way down to the GPU. Writing GPU kernels,
chasing down a few percent of throughput, and then proving the output is still
token-for-token correct is a very different kind of fun from building a CLI
tool.

If you have a Vulkan-capable GPU and a spare evening, give it a spin and see how
it compares with your current setup. Benchmarks, bug reports and PRs are all
welcome at [github.com/kryptic-sh/infr](https://github.com/kryptic-sh/infr). 🍻
