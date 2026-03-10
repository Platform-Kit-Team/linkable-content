---

title: Content Collections
published: true
---

# Content Collections

Content collections are the backbone of PlatformKit. Each collection is a set of files — Markdown, YAML, or JSON — that are processed at build time into JSON and served to the frontend.

## How it works

1. **Source files** live in `content/<collection>/` (e.g. `content/blog/`, `content/docs/`).
2. At dev startup and build time, a Vite plugin scans each directory, parses frontmatter / structured data, and writes JSON to `public/content/collections/<key>/`.
3. The Vue frontend fetches these JSON files via `fetchCollectionItems()` / `fetchCollectionItem()` from `src/lib/collections.ts`.

## Defining a collection

Collections are declared in `platformkit.config.ts` under `contentCollections`:

```ts
contentCollections: {
  projects: {
    directory: "content/projects",
    format: "yaml",
    sortField: "order",
    sortOrder: "asc",
    slugField: "title",
    fieldDefaults: { featured: false, tags: [] },
  },
},
```

### Config options

| Option          | Type                     | Description                                           |
| --------------- | ------------------------ | ----------------------------------------------------- |
| `directory`     | `string`                 | Path to source files                                  |
| `format`        | `"markdown" \            | "yaml" \                                              | "json"` | File format |
| `sortField`     | `string`                 | Field to sort the index by                            |
| `sortOrder`     | `"asc" \                 | "desc"`                                               | Sort direction |
| `slugField`     | `string`                 | Field used to generate URL slugs (default: `"title"`) |
| `recursive`     | `boolean`                | Scan subdirectories, using `_meta.json` for ordering  |
| `fieldDefaults` | `Record<string, any>`    | Default values for missing fields                     |
| `fieldRenames`  | `Record<string, string>` | Rename old fields declaratively                       |
| `indexFilter`   | `(item) => boolean`      | Filter items out of the public index                  |

## Built-in collections

PlatformKit ships with these collection types (enable/disable in theme config):

| Key          | Format               | Description                                   |
| ------------ | -------------------- | --------------------------------------------- |
| `links`      | JSON                 | Call-to-action link cards                     |
| `socials`    | Data (in model)      | Social profile icons                          |
| `gallery`    | JSON                 | Image & video gallery items                   |
| `blog`       | Markdown             | Articles with cover images, tags, RSS         |
| `resume`     | YAML                 | Structured CV (employment, education, skills) |
| `embeds`     | JSON                 | Custom HTML / iframe embeds                   |
| `docs`       | Markdown (recursive) | Hierarchical documentation                    |
| `newsletter` | Custom               | Email signup & broadcasts                     |
| `widgets`    | JSON                 | Animated text & background effects            |

## CMS editing

Each collection can define a `contentSchema` in `platformkit.config.ts` that drives the CMS editor UI (powered by FormKit). The schema controls which fields, labels, and validation rules appear in the editor drawer.

## Migrations

When you change a collection's data shape, use the migration system:

- **`fieldRenames`** — declarative, idempotent field renames.
- **`fieldDefaults`** — declarative, idempotent default values.
- **`migrations`** — imperative, version-gated transforms for complex changes.

Migrations run automatically when content is loaded. See [Configuration](/docs/introduction/configuration) for more detail on the config shape.
