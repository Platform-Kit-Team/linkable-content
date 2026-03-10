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
````

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