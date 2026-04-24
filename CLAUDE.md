# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Slidev-based presentation for the paper "Blockchain-Enabled Efficient Deduplication and Mixed Auditing for Dynamic Cloud Data" (IEEE TDSC, 2025). The project builds static slides and deploys to GitHub Pages.

## Commands

```bash
npm install          # Install dependencies
npm run dev          # Start dev server (opens browser, default http://localhost:3030)
npm run build        # Build static site to dist/
npm run export       # Export to PDF
```

## Architecture

- **`slides.md`** — Main presentation file. Frontmatter configures theme (`seriph`), transitions, and Slidev options. Content is written in Markdown with HTML/Vue intermixing, using Slidev's `---` slide separator. This is the primary file for editing slide content.
- **`components/`** — Vue 3 components (`.vue` SFCs) that can be used directly in `slides.md` via Slidev's auto-import. Currently contains `Counter.vue` and `CardBox.vue`.
- **`pages/imported-slides.md`** — Additional slide content, structured as a sub-outline of the presentation. Can be imported into `slides.md` via `src` frontmatter or referenced separately.
- **`Paper/`** — Contains the original PDF of the paper being presented.
- **`images/`** — Images referenced in slides (flow charts, gas cost charts, etc.).
- **`snippets/external.ts`** — TypeScript utility snippets usable in slides.
- **`index.md`** — A detailed Chinese-language outline/template for the presentation structure, serving as a planning document.

## Deployment

The repo supports three deployment targets; all build from `dist/`:

| Target | Config | CI/CD |
|--------|--------|-------|
| GitHub Pages | `.github/workflows/deploy.yml` | Push to `main` or manual trigger. Auto-sets `--base` using repo name. |
| Netlify | `netlify.toml` | `npm run build`, publishes `dist/` |
| Vercel | `vercel.json` | `npm run build`, output `dist/` |

## Slidev Conventions

- Slidev auto-imports Vue components from `components/` — use them directly in `slides.md` by their filename (e.g., `<Counter />`, `<CardBox>`).
- Frontmatter per-slide: use `hideInToc: true` to exclude from table of contents, `class: text-center` for centered layouts.
- Inline styles use Slidev's shorthand syntax (e.g., `flex="~"`, `border="~ main rounded-md"`, `hover:bg="gray-400 opacity-20"`).
- Theme is `seriph`; drawings persistence is disabled.
