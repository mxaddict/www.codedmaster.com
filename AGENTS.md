# AGENTS.md

This file provides guidelines for agentic coding agents operating in this
repository.

## Project Overview

This is a static website built with [Zola](https://www.getzola.org/), a fast,
Rust-based static site generator. The site showcases blog posts and technical
content.

## Build/Lint/Test Commands

- **Build site:** `zola build`
  - Output goes to the `public/` directory
- **Serve site locally:** `zola serve` (usually at <http://127.0.0.1:1111>)
- **Build & deploy:** `./build`
- **Create new blog post:**
  `touch content/blog/$(date +%Y-%m-%d)-post-title-slug.md`
- **Check Zola installation:** `zola version`

## Code Style Guidelines

### General

- Uses Markdown files for content (`.md`)
- Follows Zola's templating system with HTML and Liquid syntax
- Content organized in `content/blog/` directory with date-based filenames
- Static assets in `static/` directory
- Theme-based styling in `themes/` directory

### File Naming

- Blog posts use format: `YYYY-MM-DD-post-title-slug.md`
- All files use lowercase letters and hyphens (kebab-case)
- Content structure follows Zola conventions

### Formatting

- Files use UTF-8 encoding
- Two-space indentation (as per .editorconfig)
- LF line endings
- Trailing whitespace removed
- Final newline required

### Code Style

- Uses Prettier for consistent formatting
- Single quotes preferred
- Trailing commas in objects/arrays
- Print width of 80 characters

### Content Structure

- YAML frontmatter for posts with `title`, `date`, and `tags`
- Content organized in blog categories under `content/blog/`
- Uses taxonomies for tags categorization
- Theme configurations in `zola.toml` file

### Error Handling

- No traditional error handling required as this is a static site generator
- Build scripts check for required tools (Zola) before proceeding
- Deployment script handles Git operations and pushes to GitHub Pages

## Additional Configuration

- Theme: `zolanight`
- Taxonomies: tags
- Markdown highlighting with "catppuccin-mocha" theme
- Google Analytics integration
- Kofi donation link support

## Development Workflow

1. Make changes in content directory
2. Run `zola serve` to preview changes locally
3. Commit and use `./build` for deployment
