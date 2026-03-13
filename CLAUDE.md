# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal portfolio and blog site built with [Zola](https://www.getzola.org/) (Rust-based static site generator) using the Redux theme (a fork of Apollo). Deployed to GitHub Pages via GitHub Actions on push to `main`.

- Site URL: `https://www.charlo.tech`
- Theme: `themes/redux/` (git submodule — `https://github.com/seniormars/redux`)

## Commands

```bash
zola serve       # Local dev server at http://localhost:1111 (live reload)
zola build       # Build static site to /public
zola check       # Validate config and check for broken links
```

Deployment is automatic: pushing to `main` triggers `.github/workflows/main.yml`, which builds and deploys to the `gh-pages` branch.

## Architecture

### Content (`/content/`)
Markdown files with TOML frontmatter. Three main sections:
- `posts/` — blog articles, sorted by date, paginated (7/page)
- `projects/` — portfolio items, sorted by `weight`, rendered as cards via `cards.html`
- `about.md` — single about page

### Templates (`/templates/`)
Zola uses Tera templating. Files here **override** the Redux theme's templates. Key files:
- `base.html` — master layout
- `macros/macros.html` — reusable macros for post rendering and card layouts
- `partials/header.html` — `<head>` metadata, analytics, fonts
- `partials/nav.html` — navigation and theme toggle
- `shortcodes/` — custom markdown shortcodes (`image`, `video`, `note`, `youtube`, etc.)

### Configuration (`config.toml`)
All site settings live here: theme, navigation links, social links, feature flags (MathJax, Giscus comments, syntax highlighting, smart punctuation). Theme-specific options go under `[extra]`.

### Theme customization
The Redux theme is a git submodule — do not modify files under `themes/redux/` directly. Override theme behavior by placing identically-named files in the top-level `templates/` directory.
