# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

TrailStories — Sebastian's personal mountainbiking blog (racing, training, gear). Static site built with Jekyll, deployed via Netlify.

## Commands

```bash
bundle install              # install gems (first time / after Gemfile change)
bundle exec jekyll serve    # local dev server, live rebuild, http://localhost:4000
bundle exec jekyll build    # build static site into _site/
```

No test suite, linter, or CI config in this repo.

## Architecture

Standard Jekyll structure:

- `_posts/` — blog posts, one file per post, named `YYYY-MM-DD-title.md` with `layout: post` front matter (`title`, `date`, `tags`). This is almost all the content work in this repo.
- `_layouts/` — `default.html` (base template), `home.html`, `page.html`, `post.html`, `tags.html`.
- `_includes/` — shared partials pulled into layouts (head, header, footer, social icons, Disqus comments, Google Analytics).
- `_sass/` + `assets/main.scss` — styling. `trailstories/` holds this site's own SCSS partials; `minima/` is the base theme's SCSS being customized/overridden.
- `assets/` — images referenced by posts, plus PWA icons.
- `_config.yml` — site-wide settings (title, url, social usernames, plugins: `jekyll-feed`). Not reloaded by `jekyll serve` — restart the server after editing it.
- `tags.md` — tag index page (`layout: tags`).
- `manifest.json`, `service-worker.js` — basic PWA support.

## Writing a new post

Copy the front matter pattern from an existing `_posts/*.md` file:

```yaml
---
layout: post
title: "Post Title"
date: YYYY-MM-DD
tags: race mtb
---
```

Cross-link older posts with `{% post_url YYYY-MM-DD-filename %}`.
