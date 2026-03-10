---
title: CSS Variables
published: true
---

# CSS Variables

PlatformKit themes are styled with CSS custom properties. You can tweak every colour, font, and spacing value through the CMS theme editor — or by setting variables directly in your override config.

## Colour variables

| Variable | Description | Example (dark) |
|----------|-------------|----------------|
| `--bg` | Page background | `#0a0a0a` |
| `--color-brand` | Primary brand colour | `#6366f1` |
| `--color-brand-strong` | Stronger brand variant | `#818cf8` |
| `--color-accent` | Accent / highlight | `#f59e0b` |
| `--color-ink` | Main text colour | `#f5f5f5` |
| `--color-ink-soft` | Muted / secondary text | `#a3a3a3` |
| `--glass` | Glass surface (semi-transparent) | `rgba(255,255,255,0.05)` |
| `--glass2` | Alternate glass surface | `rgba(255,255,255,0.08)` |
| `--glassStrong` | More opaque glass | `rgba(255,255,255,0.12)` |
| `--color-border` | Border colour | `rgba(255,255,255,0.1)` |
| `--color-border2` | Secondary border | `rgba(255,255,255,0.06)` |
| `--card-bg` | Card background | `rgba(24,24,27,0.8)` |
| `--card-border` | Card border | `rgba(255,255,255,0.08)` |
| `--card-text` | Card text colour | `#e5e5e5` |

## Typography variables

| Variable | Description | Example |
|----------|-------------|---------|
| `--font-family` | Base font stack | `"Inter", sans-serif` |
| `--font-weight` | Default font weight | `400` |
| `--letter-spacing` | Base letter spacing | `0em` |

## Bento layout variables

| Variable | Default | Description |
|----------|---------|-------------|
| `--bento-grid-width` | `960px` | Maximum grid width |
| `--bento-gap` | `16px` | Space between grid cells |
| `--bento-card-radius` | `20px` | Card corner radius |
| `--bento-card-bg` | `var(--card-bg)` | Card background |
| `--bento-card-border` | `var(--card-border)` | Card border |
| `--bento-card-shadow` | `none` | Card box shadow |
| `--bento-hover-scale` | `1.02` | Card hover zoom factor |

## Setting variables in the CMS

1. Double-click the profile header to open the admin panel.
2. Navigate to **Theme** settings.
3. Pick a preset (Light, Dark, or Custom).
4. Adjust individual colour values using the colour pickers.
5. Save — changes apply immediately.

## Setting variables via config

In `src/overrides/platformkit.config.ts`, you can define variables programmatically through the theme's `layoutData` structure. Each theme documents which fields map to which CSS variables.

## Tips

- Use `var(--color-brand)` in your own components to stay consistent with the active theme.
- The `--glass*` variables are composited with `backdrop-filter: blur()` for the glassmorphism effect.
- Override variables at the `:root` level in a custom stylesheet if you need full CSS control.
