+++
title = "Why I Switched: Migrating My Blog from Jekyll to Zola"
date = 2026-01-24
description = "Learn about the reasons and process behind migrating a personal tech blog from Jekyll to Zola, highlighting performance gains, Rust's benefits, and Zola's features."
[taxonomies]
tags = ["jekyll", "zola", "static site generator", "migration", "web development", "rust"]
[extra]
author = "mxaddict"
+++

For a while now, my blog has been running on Jekyll, a solid static site
generator that's been around for ages. It served me well, powering this corner
of the internet where I share thoughts on Linux, CLI tools, web development, and
the occasional motorcycle musing. But as my needs evolved and my desire for
faster build times and a more streamlined workflow grew, I started looking for
alternatives. That's when Zola caught my eye.

### Why Migrate? The Pull Towards Zola

Jekyll is fantastic, but over time, I found myself wanting a few things that
Zola seems to offer more directly:

- **Build Speed:** As my content grew, Jekyll's build times started to creep up.
  I wanted something snappier, something that felt more responsive even when
  generating a hundred pages.
- **Single Binary:** The idea of a single executable for a static site generator
  is incredibly appealing. No complex Ruby environment to manage, no version
  conflicts. Just download, run, and go. This resonates heavily with my
  CLI-first workflow.
- **Rust Ecosystem:** I'm increasingly drawn to Rust's performance, safety, and
  concurrency guarantees. Zola being built in Rust meant it likely offered
  excellent performance and reliability.
- **Simplicity and Features:** Zola's templating language (Tera) is powerful,
  and its built-in features like shortcodes and its handling of sections and
  pages felt very intuitive.

### The Migration Process: Less Painful Than Expected

Migrating from Jekyll to Zola involved a few key steps:

1. **Content Conversion:** Jekyll uses Liquid templating and typically Markdown
   files with TOML front matter. Zola uses Tera templating and TOML front
   matter. The transition for most Markdown files was straightforward. The main
   effort was ensuring front matter was correctly translated, especially for
   tags and dates.
2. **Theme Adaptation:** I found a theme that fit my aesthetic – `anemone`.
   Adapting it involved understanding its template structure and making minor
   tweaks to fit my content organization.
3. **Configuration:** Translating `_config.yml` settings to `zola.toml` was
   relatively simple, with Zola's configuration structure being quite clear.

The biggest hurdle was ensuring my content structure matched Zola's
expectations, especially for the blog section. As we've seen, getting Zola to
recognize a `blog` section and its posts correctly requires careful setup.

### Zola's Benefits in Practice

Since switching, the difference has been noticeable:

- **Build Times:** Zola's build times are blazingly fast. Whether I'm making a
  small change or a large update, the site regenerates in seconds.
- **Simplicity:** Managing Zola is a breeze. A single binary means no dependency
  hell.
- **Performance:** The generated static sites are incredibly performant.

### Final Thoughts

Migrating from Jekyll to Zola has been a positive experience. It aligned
perfectly with my preference for fast, efficient tools and a CLI-centric
workflow. If you're looking for a modern, high-performance static site
generator, Zola is definitely worth considering.
