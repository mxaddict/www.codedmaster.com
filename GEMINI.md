# Project Context for Gemini CLI

This project is a personal blog built with [Zola](https://www.getzola.org/), a
static site generator.

## Key Information

- **Website URL:** <https://www.codedmaster.com>
- **Theme:** `anemone` (located in `themes/anemone/`)
- **Content Directory:** `content/`
    - Blog posts are typically found in `content/blog/`.
    - Pages like "about" and "journal" are in `content/about.md` and
      `content/journal.md`.
- **Static Assets:** `static/` (for images, CSS, JS not part of the theme).
- **Zola Configuration:** `zola.toml`
- **Taxonomies:** `tags` (used for categorizing posts).

## Common Commands

- **Build the site:** `zola build`
    - Output goes to the `public/` directory.
- **Build & Deploy the site:** `./build`
    - Deploys the static code in `public/` to github pages
- **Serve the site locally:** `zola serve`
    - Starts a local development server, usually accessible at
      `http://127.0.0.1:1111`.
    - Includes live-reloading.
- **Create a new blog post:**

    ```bash
    touch content/blog/$(date +%Y-%m-%d)-post-title-slash-slug.md
    ```

## Instructions for Gemini

When I ask you to perform tasks related to this project, please consider the
following:

- **Zola Front Matter:** I use TOML for the front matter not YML
- **Zola Best Practices:** Adhere to Zola's conventions for content, templates,
  and configuration.
- **Markdown:** Assume content files are written in Markdown.
- **File Paths:** When referencing files, use paths relative to the project root
  unless specified otherwise.
- **New Content:** When creating new content, assume it should be in
  `content/blog/` unless I specify a different section.
- **Testing:** After making changes, especially to content or templates run
  `zola build` for local testing. Then fix any issues/errors if `zola build`
  fails or has warnings

---

**Note to Gemini:** This `GEMINI.md` file provides essential context. Please
refer to it for understanding the project's structure and my preferences when
assisting me.
