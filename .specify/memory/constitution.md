# TrailStories Constitution

## Core Principles

### I. Static-First, No Runtime Backend

- The site MUST remain a pure static Jekyll build deployed via Netlify; no server-side runtime,
  database, or build-time secrets in the repo.
- Dynamic behavior MUST be limited to small, progressive-enhancement client JS or third-party
  embeds already in use (Disqus, PostHog). Every page MUST be fully readable without JS.
- Plugins MUST be limited to those supported by the Netlify Jekyll build; adding a gem MUST be
  justified by need and maintenance status.

Rationale: a personal blog is cheapest and most durable as plain files over a CDN.

### II. Content Is the Product

- Posts live in `_posts/YYYY-MM-DD-title.md` with `layout: post` and front matter `title`,
  `date`, `tags`. Tags MUST reuse existing tags where one fits.
- Cross-links between posts MUST use `{% post_url YYYY-MM-DD-filename %}`, never hardcoded URLs.
- Images MUST live under `assets/`, MUST have meaningful alt text, and SHOULD be resized/compressed
  before commit (no multi-MB originals).
- Published posts and their URLs MUST NOT break; renaming/removing a post requires a redirect or
  explicit justification.
- Author voice and facts (race results, gear, dates) MUST NOT be invented; unknown facts are
  asked for, not guessed.

Rationale: readers and old links are the long-term value; code exists to serve posts.

### III. Privacy & Consent

- Tracking and third-party embeds MUST respect EU/GDPR requirements (site is operated from
  Germany). Any new tracker, cookie, or third-party widget MUST be flagged for consent/privacy
  policy impact (`imprint.md`, privacy text) before shipping.
- No personal data beyond what PostHog and Disqus already process MAY be collected.

### IV. Accessible, Fast, Responsive

- Layouts MUST be semantic HTML, keyboard-navigable, with sufficient contrast and working at
  mobile widths.
- Pages MUST stay lightweight: no large JS frameworks, lazy-load below-the-fold images where
  practical, no layout-shifting embeds.
- PWA assets (`manifest.json`, `service-worker.js`) MUST keep working; bump the cache version
  when cached asset URLs change.

### V. Minimal, Consistent Theming

- Styling changes go in `_sass/trailstories/` and `assets/main.scss`; `_sass/minima/` is the
  base theme and SHOULD only be overridden, not forked piecemeal.
- Reuse existing includes/layouts before adding new ones; prefer simple Liquid over plugins.

### VI. Verified Builds

- There is no test suite or CI. Every change MUST be verified with `bundle exec jekyll build`
  succeeding without new warnings; visual/layout changes MUST also be checked via
  `bundle exec jekyll serve`.
- `_config.yml` changes require a server restart to take effect.

## Technical Constraints

- Stack: Jekyll (Ruby, Bundler), Liquid, Markdown, SCSS, Netlify hosting.
- Build output `_site/`, `.jekyll-cache`, `.sass-cache`, `vendor`, `.netlify`, `.env*` MUST stay
  gitignored.
- Do not add Node/JS toolchains, test frameworks, or linters unless a spec justifies it.

## Development Workflow

- Routine content work (new posts, typo fixes, image additions) does NOT need spec-kit; just
  edit and build.
- Non-trivial site changes (layout/theme redesign, new page types, new integrations, SEO/PWA
  work) SHOULD go through `/speckit-specify` → `/speckit-plan` → `/speckit-tasks` →
  `/speckit-implement`; artifacts live under `.specify/` and `specs/`.
- Plans MUST state impact on privacy/consent, page weight, and existing URLs, or state none.
- Commits SHOULD be short, imperative, and descriptive of the change (e.g. "Add photos to
  Wörthersee Gravel Race post").

## Governance

This constitution supersedes other practices. `CLAUDE.md` provides runtime guidance for agents
and MUST stay consistent with it. Amendments require updating this file with a version bump and
date.

**Version**: 1.0.0 | **Ratified**: 2026-10-13 | **Last Amended**: 2026-10-13
