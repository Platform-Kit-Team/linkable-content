---

title: Overrides
published: true
---

# Overrides

The **overrides** layer lets you customise your site without touching the theme source code. Everything in `src/overrides/` takes priority over theme defaults.

## What you can override

### Configuration

Create `src/overrides/platformkit.config.ts` to override any config value:

```ts
import type { PlatformKitConfig } from "../../lib/config";

const config: PlatformKitConfig = {
  // Enable or disable collections
  contentCollections: {
    gallery: {
      directory: "content/gallery",
      format: "json",
      sortField: "order",
      sortOrder: "asc",
    },
  },
  // Add custom build hooks
  buildHooks: [
    {
      name: "my-custom-hook",
      stage: "afterBuild",
      handler: async (ctx) => {
        console.log("Build finished!");
      },
    },
  ],
};

export default config;
```

Config values are deep-merged: system → theme → overrides. You only need to specify the fields you want to change.

### Components

Place Vue components in `src/overrides/` to replace theme-level components. The theme resolver checks overrides first, falling back to the theme directory.

### Dependencies

If your overrides need additional npm packages, create `src/overrides/package.json`:

```json
{
  "name": "@overrides/my-site",
  "private": true,
  "dependencies": {
    "some-library": "^1.0.0"
  }
}
```

These are installed automatically alongside theme dependencies.

## When to use overrides vs. a custom theme

| Use overrides when…                                        | Use a custom theme when…                        |
| ---------------------------------------------------------- | ----------------------------------------------- |
| Tweaking config values (colours, collections, build hooks) | Rebuilding the entire layout from scratch       |
| Replacing one or two components                            | Changing navigation, routing, or page structure |
| Adding extra build hooks                                   | Creating a reusable layout for multiple sites   |
| Site-specific customisations                               | Sharing with others as a template               |

---

## Customizing Theme & Override Paths

By default, themes live in `src/themes/` and overrides in `src/overrides/`. All component, theme, and override discovery uses static glob patterns for both core and user directories:

- `../themes/**/*.vue` and `../themes/user/**/*.vue` for theme components
- `../overrides/*.vue` and `../overrides/user/*.vue` for overrides
- `../themes/**/platformkit.config.ts` and `../themes/user/**/platformkit.config.ts` for theme configs

Dynamic template literals are not supported anywhere in Vite glob imports. Both core and user directories are always scanned, so to add custom themes or overrides, stage them in `src/themes/`, `src/themes/user/`, `src/overrides/`, or `src/overrides/user/`. The resolver will automatically discover and prioritize these directories.

If you want to use custom directories (for example, to stage user-provided themes/overrides), you can specify paths in your `platformkit.config.ts`, but they must be subdirectories of the fixed paths.

```ts
const config: PlatformKitConfig = {
  paths: {
    themeDir: "src/themes",      // default
    overrideDir: "src/overrides" // default
  },
  // ...other config...
};
```

If you stage user themes in `src/themes/user/` and overrides in `src/overrides/user/`, these will be automatically discovered and prioritized above core themes/overrides. The resolution order is:

1. `src/overrides/user/<Name>.vue` (user overrides)
2. `src/overrides/<Name>.vue` (core overrides)
3. `src/themes/user/<layout>/<Name>.vue` (user themes)
4. `src/themes/<layout>/<Name>.vue` (core themes)
5. fallback (default component)

You can change `themeDir` and `overrideDir` to point to any directory you want. All theme and override discovery will use these paths.

> **Note:** User-provided themes and overrides are typically staged by the CLI into `/src/themes/user/` and `/src/overrides/user/` and are `.gitignore`d to avoid contaminating the core repo.