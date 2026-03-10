---

title: GitHub Sync
published: true
---

# GitHub Sync

PlatformKit can sync your content (CMS data, uploads, blog posts, collections) to a private GitHub repository. This gives you version-controlled backups and enables CI/CD deployment workflows.

## Setup

1. **Create a private GitHub repo** for your content.
2. **Generate a Personal Access Token** with `repo` scope.
3. In the CMS admin panel, open **Settings** → **GitHub** and enter:
   - GitHub username / organisation
   - Repository name
   - Personal access token (encrypted locally with PBKDF2 + AES-256-GCM)

## Push & pull

### Push (export to GitHub)

```bash
pnpm push            # or: npm run push
```

This runs `scripts/export-to-github.mjs`, which:

1. Exports `cms-data.json` and all content directories.
2. Commits and pushes to the configured GitHub repo.

### Pull (import from GitHub)

```bash
pnpm import          # or: npm run import
```

This runs `scripts/import-from-github.mjs`, which:

1. Pulls the latest content from the GitHub repo.
2. Writes files to `cms-data.json`, `content/`, and `public/content/uploads/`.

The import step also runs automatically at the start of every build, so deployed sites always use the latest content.

## What gets synced

| Content                                | Location                      | Synced?                  |
| -------------------------------------- | ----------------------------- | ------------------------ |
| CMS data (profile, theme, collections) | `cms-data.json`               | ✅                        |
| Blog posts (Markdown)                  | `content/blog/`               | ✅                        |
| Docs (Markdown)                        | `content/docs/`               | ✅                        |
| Other collections                      | `content/<key>/`              | ✅                        |
| Uploaded images & media                | `public/content/uploads/`     | ✅                        |
| Built JSON output                      | `public/content/collections/` | ❌ (regenerated at build) |
| RSS, OG HTML                           | `public/content/`             | ❌ (regenerated at build) |

## Security

- Your GitHub token is encrypted client-side before storage.
- Tokens are never committed to the repo.
- The private repo should not be shared publicly.

## CMS commit UI

In the CMS, the **Git** button in the toolbar opens a commit dialog. This lets you push changes directly from the browser without using the terminal.
