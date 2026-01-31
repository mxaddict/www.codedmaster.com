+++
date = 2026-01-31
title = "From Zero to Website: How Easy It Is to Get Started with Zola"
description = "A quick-start guide to building your first static website with Zola, covering installation, project setup, theme integration (featuring ZolaNight), adding content, and local serving."
[taxonomies]
tags = ["zola", "static site generator", "web development", "tutorial", "getting-started", "zolanight"]
+++

Dreaming of a fast, secure, and easy-to-manage website or blog? Look no further
than [Zola](https://www.getzola.org/), a blazing-fast static site generator
built with Rust. In this tutorial, I'll show you just how simple it is to go
from zero to a fully functional website in minutes.

Let's dive in!

## Step 1: Install Zola

First things first, you need Zola itself. It's a single binary, making
installation a breeze.

**For Arch Linux users:**

```bash
sudo pacman -S zola
```

**For macOS users (using Homebrew):**

```bash
brew install zola
```

If you're on another operating system, check the
[official Zola documentation](https://www.getzola.org/documentation/getting-started/installation/)
for detailed installation instructions.

## Step 2: Create a New Website

Once Zola is installed, you can create a new site project with a single command:

```bash
zola init my-new-website
cd my-new-website
```

Zola will ask you a few questions, like your site's URL and whether you want a
`config.toml` file (just hit Enter for the defaults for now). This command sets
up the basic directory structure for your new site.

## Step 3: Add a Zola Theme (Self-Plug: ZolaNight!)

A theme gives your Zola site its look and feel. There are many great themes
available, but since you're here, why not try my very own minimalist and fast
theme, [ZolaNight](https://zolanight.codedmaster.com/)?

First, add the theme to your project:

```bash
git init # If you haven't already
git submodule add https://github.com/mxaddict/zolanight.git themes/zolanight
```

Next, open your `config.toml` file (created in Step 2) and tell Zola to use the
new theme. Add or modify the `theme` line:

```toml
# config.toml
base_url = "http://localhost:1111" # Or your actual site URL
title = "My Awesome Zola Site"
theme = "zolanight"
```

## Step 4: Add Your Content

A website isn't much without content! Zola uses Markdown files in the `content`
directory. Let's create a homepage and a second page.

### The Homepage

To create the content for your main landing page, you need to create a special
file named `_index.md` inside the `content` directory.

Create `content/_index.md` with the following:

```markdown
+++
title = "Welcome to My Awesome Zola Site!"
date = 2026-01-31
description = "This is the homepage of my new Zola site. So easy!"
+++

Hello, world! This is my homepage. It was incredibly easy to set up!

You can write your content using **Markdown**.
```

### A Second Page

Now, let's add another page. Any other `.md` file in the `content` directory will
become a separate page on your site.

Create `content/second-page.md` with the following:

```markdown
+++
title = "This is My Second Page"
date = 2026-01-31
description = "Another page to show how Zola works."
+++

This is another page on the website. Zola will generate a URL for it
automatically, something like `/second-page/`.
```

## Step 5: Run "zola serve" and See Your Website

Now for the magic moment! To see your website locally, simply run:

```bash
zola serve
```

This command will start a local development server, usually accessible at
`http://127.0.0.1:1111`. Open your web browser to this address, and you'll see
your brand new Zola site, complete with the ZolaNight theme and your first
content page!

Zola also includes live-reloading, so any changes you make to your content or
configuration files will automatically update in your browser.

## Conclusion

In just a few simple steps, you've installed Zola, set up a new project,
integrated a theme, added content, and viewed it all locally. Zola's speed,
simplicity, and powerful features make it an excellent choice for anyone looking
to build a modern static website.

Happy Zola-ing!
