---
section: Introduction
_path: introduction
published: true
title: Getting Started
---
## Extensibility

PlatformKit is designed for easy extension:
- **Themes:** Add new themes in `src/themes/` or your content repo.
- **Overrides:** Replace any component via `src/overrides/`.
- **Build Hooks:** Extend the build process (TTS, image optimization, OG meta, etc.) via config.
- **Custom Collections:** Add new content types via config.
- **Widgets:** Add animated text/backgrounds via CMS or theme config.
- **Docs:** Add new docs pages in `content/docs/`, organize with `_meta.json`.
- **Error Handling:** See TODO.md for known issues and mitigations.
## Build Hooks

Build hooks run during `vite build` and let you automate tasks like TTS audio, image optimization, OG meta generation, etc. Register hooks in your theme or user config under `buildHooks`.
## Custom Collections

Add new collections by editing your config file. Collections support schema migrations, validation, custom editors, and build hooks. See `src/lib/config.ts` for options.
## Widget System

Widgets are animated text, backgrounds, and interactive elements. Extend via CMS or theme config. See `src/themes/bento/platformkit.config.ts` for schema options.
## Docs Extensibility

Docs are markdown files in `content/docs/`. Add pages, organize with `_meta.json`. Sidebar/nav tree is auto-generated.
## Error Handling & Security

CMS endpoints are UI-protected only; server-side auth is not enforced. File uploads are validated for type, size, and path. Passwords are encrypted in session storage. See TODO.md for known issues and recommended mitigations.
---

published: true
title: Getting Started
---

# Getting Started

PlatformKit is a modular personal site builder powered by Vue 3, Vite, and Tailwind CSS. It ships with a built-in CMS, theming system, and a growing library of content collections — links, blog, gallery, resume, docs, newsletter, embeds, and more.

## Prerequisites

- **Node.js** v22 or later (see `.nvmrc`)
- **pnpm** (recommended) or npm

## Installation

Clone the repo and install dependencies:

```bash
git clone <your-repo-url> my-site
cd my-site
pnpm install        # or: npm install
```

Theme- and override-specific dependencies are installed automatically by `scripts/install-layout-deps.mjs` — you don't need to install them manually.

## Start the dev server

```bash
pnpm dev            # or: npm run dev
```

Open [http://localhost:8080](http://localhost:8080) in your browser. You'll see the default Bento layout with placeholder content.

## Project structure at a glance

````
├── src/
│   ├── themes/bento/       # Active theme (layout + config)
│   ├── overrides/          # Your local customisation layer
│   ├── components/         # Shared UI components
│   ├── lib/                # Core library (model, collections, config)
│   └── pages/              # Entry page
├── content/                # Your markdown & YAML content (gitignored)
├── public/content/         # Build output for content (gitignored)
├── cms-data.json           # Local CMS working copy
├── default-data.json       # Seed data (committed)
└── platformkit.config.ts   # Root-level configuration
```

- `src/themes/` — theme layouts (configurable via `platformkit.config.ts`)
- `src/overrides/` — global component overrides (configurable via `platformkit.config.ts`)
- `src/themes/user/` — user-provided themes (staged by CLI, prioritized)
- `src/overrides/user/` — user-provided overrides (staged by CLI, prioritized)

You can change the theme and override directories by setting `themeDir` and `overrideDir` in your `platformkit.config.ts`. All theme and override discovery will use these paths.

## Using the CMS

Double-click the **profile header** (avatar / name area) to open the admin panel. From there you can:

- Edit your profile (name, tagline, avatar, banner)
- Manage links, embeds, gallery items, blog posts, and more
- Switch theme presets (light / dark) and tweak CSS variables
- Commit changes to GitHub (if a token is configured)

## Next steps

- [Configuration](/docs/introduction/configuration) — learn how the three-level config system works
- [Content Collections](/docs/content/collections) — understand how content is stored and rendered
- [Themes](/docs/customization/themes) — create or modify a theme
