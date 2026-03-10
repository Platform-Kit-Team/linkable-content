---
title: Supabase
published: true
---

# Supabase Integration

PlatformKit uses [Supabase](https://supabase.com) as an optional backend for features that need server-side logic: newsletter management, visitor analytics, and subscriber data storage.

## Local development

Start the local Supabase stack:

```bash
npm run supabase:start
```

This launches a local PostgreSQL 17 database, Auth, and Edge Functions runtime via Docker.

### Applying migrations

```bash
npm run supabase:migrate:up
```

This runs `npx supabase migration up --local` and applies only **pending** migrations. It never resets or drops existing data.

> **Warning:** Never use `supabase db reset` — it destroys all data. Always use `migrate:up`.

### Serving edge functions

```bash
npm run supabase:functions
```

This starts the edge functions dev server so you can test newsletter signup, confirmation, and analytics locally.

### Generating types

```bash
npm run supabase:types
```

Generates TypeScript type definitions from your database schema.

## Edge functions

| Function | Purpose |
|----------|---------|
| `newsletter-signup` | Handle public email subscriptions |
| `newsletter-confirm` | Verify confirmation links |
| `newsletter-admin` | CRUD for subscribers and broadcasts |
| `newsletter-send` | Batch-send scheduled broadcasts |
| `newsletter-cron` | Scheduled task runner |
| `newsletter-unsubscribe` | Handle unsubscribe links |
| `newsletter-view` | Render newsletter archive pages |
| `newsletter-worker` | Async queue worker for email sends |

## Analytics

When Supabase is configured, PlatformKit tracks:

- **Page views** — URL, referrer, timestamp
- **Link clicks** — which links visitors interact with
- **Visitor identity** — stable browser fingerprint (via FingerprintJS), no personal data

Analytics data is sent fire-and-forget and never blocks the UI. View analytics in the CMS admin panel under **Analytics**.

## Hosted Supabase

For production, create a project at [supabase.com](https://supabase.com) and set these environment variables:

```bash
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-anon-key
```

Apply migrations to the hosted database with:

```bash
npx supabase db push --linked
```

## Configuration

Supabase settings live in `supabase/config.toml`. Key values:

- **`project_id`** — your Supabase project ID
- **`[api]`** — API port and settings
- **`[db]`** — database port and connection details
- **`[auth]`** — authentication settings
