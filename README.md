# <www.codedmaster.com>

This is my personal website, powered by [Zola](https://www.getzola.org/), a
fast, Rust-based static site generator. The site showcases my interests in CLI
tools, code, and various tech insights.

## Key Information

- **Website URL:** <https://www.codedmaster.com>
- **Theme:** `zolanight` (located in `themes/zolanight/`)
- **Content Directory:** `content/`
  - Blog posts are typically found in `content/blog/`.
- **Static Assets:** `static/` (for images, CSS, JS not part of the theme).
- **Zola Configuration:** `zola.toml`
- **Taxonomies:** `tags` (used for categorizing posts).

## Common Commands

- **Build the site:** `zola build`
  - Output goes to the `public/` directory.
- **Build & Deploy the site:** `./build`
  - Deploys the static code in `public/` to GitHub Pages.
- **Serve the site locally:** `zola serve`
  - Starts a local development server, usually accessible at
      `http://127.0.0.1:1111`.
  - Includes live-reloading.
- **Create a new blog post:**

    ```bash
    touch content/blog/$(date +%Y-%m-%d)-post-title-slash-slug.md
    ```

## License

[MIT license](LICENSE).
