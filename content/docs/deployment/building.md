---

title: Building & Deploying
published: true
---

# Building & Deploying

PlatformKit builds to a fully static `dist/` folder that you can deploy to any static hosting provider.

## Build commands

```bash
# Production build
pnpm build           # or: npm run build

# Development build (unminified, with source maps)
pnpm build:dev       # or: npm run build:dev

# Preview the production build locally
pnpm preview         # or: npm run preview
```

## What happens during build

1. **Dependency install** — `scripts/install-layout-deps.mjs` installs any extra packages declared in theme or override `package.json` files.
2. **Content import** — `scripts/import-from-github.mjs` pulls content from your private GitHub repo (if configured).
3. **Data export** — `scripts/export-data.mjs` writes `cms-data.json` → `public/content/data.json`.
4. **Vite build** — compiles Vue, TypeScript, and Tailwind; runs build hooks:
   - **Collection build** — scans `content/` directories, generates JSON to `public/content/collections/`.
   - **Image optimisation** — compresses uploads to AVIF/WebP (1920 × 1920 max, 80 % quality).
   - **RSS generation** — produces `public/content/rss.xml` for the blog.
   - **OG pre-render** — generates per-post HTML shells for social media crawlers.
   - **TTS** — (optional) generates MP3 audio from blog post text.
5. **Static output** — everything lands in `dist/`, ready to serve.

## Deploying to popular hosts

### Netlify

The repo includes a `public/_redirects` file for SPA fallback. To deploy:

1. Connect your repo to Netlify.
2. Set **Build command** → `npm run build`
3. Set **Publish directory** → `dist`
4. Deploy.

### Vercel

1. Import the repo into Vercel.
2. Framework preset: **Vite**.
3. Build command: `npm run build`, output: `dist`.

### GitHub Pages

1. Build locally or via GitHub Actions.
2. Push the `dist/` folder to a `gh-pages` branch.
3. Enable GitHub Pages from repository settings.

### Self-hosted (nginx)

A helper script is included:

```bash
./scripts/serve-nginx.sh
```

Or configure nginx manually to serve `dist/` with SPA fallback:

```nginx
location / {
    root /path/to/dist;
    try_files $uri $uri/ /index.html;
}
```

### CLI deployment (npx)

You can deploy your site using the PlatformKit CLI without installing anything globally:

```bash
npx platformkit deploy
```

This command builds your site and deploys it to your configured target (Netlify, Vercel, GitHub Pages, or custom). The CLI auto-detects your project type and walks you through any required setup.

> Tip: Use `npx platformkit deploy --help` for all available options.

## Environment variables

| Variable            | Purpose                                          |
| ------------------- | ------------------------------------------------ |
| `GITHUB_TOKEN`      | GitHub personal access token for content sync    |
| `GITHUB_OWNER`      | GitHub username / org                            |
| `GITHUB_REPO`       | Repository name for content storage              |
| `SUPABASE_URL`      | Supabase project URL (for newsletter, analytics) |
| `SUPABASE_ANON_KEY` | Supabase anonymous key                           |