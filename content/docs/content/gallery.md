---

title: Gallery
published: true
---

# Gallery

The gallery collection displays images and videos in a responsive masonry grid with lightbox viewing, tag filtering, and hover effects.

## Adding gallery items

Gallery items are stored as JSON files (managed through the CMS), or you can create them manually:

```json
{
  "title": "Mountain Sunrise",
  "imageUrl": "/content/uploads/mountain.avif",
  "tags": ["nature", "photography"],
  "description": "Shot at dawn from the summit trail.",
  "published": true,
  "order": 1
}
```

## Supported media

### Images

Upload images through the CMS. The build-time image optimisation hook automatically converts them to AVIF/WebP and constrains dimensions to 1920 × 1920 at 80 % quality.

### Videos

Embed videos by providing a URL:

- **YouTube** — paste a `youtube.com/watch?v=...` or `youtu.be/...` link
- **Vimeo** — paste a `vimeo.com/...` link
- **Self-hosted MP4** — provide a direct `.mp4` URL

Videos display inline with a play button overlay. Clicking opens a full-screen video player.

## Layout

The Bento theme renders the gallery as a **masonry grid** with:

- Alternating hero rows (one large image spanning multiple columns) and regular rows
- Auto-dense grid packing
- Configurable gap and card radius via CSS variables
- Hover zoom effect (`--bento-hover-scale`)
- Title and description overlay on hover

## Filtering & search

If gallery items have `tags`, a tag filter bar appears above the grid. Users can select one or more tags to narrow results. A search bar provides full-text filtering across titles and descriptions.

## Lightbox

Clicking an image opens a full-screen lightbox overlay with:

- High-resolution image display
- Close button or click-outside to dismiss
- Keyboard navigation (Escape to close)