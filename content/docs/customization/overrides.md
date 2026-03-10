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

| Use overrides when… | Use a custom theme when… |
|---------------------|--------------------------|
| Tweaking config values (colours, collections, build hooks) | Rebuilding the entire layout from scratch |
| Replacing one or two components | Changing navigation, routing, or page structure |
| Adding extra build hooks | Creating a reusable layout for multiple sites |
| Site-specific customisations | Sharing with others as a template |
