---
description: "Adding a subtle 1px outline to images for depth and visual consistency, using transparent outline with inset offset."
title: Image Outlines
---

# Image Outlines

Images placed directly on a background can feel like they're floating without anchor. A `1px` outline at low opacity creates a subtle boundary that adds depth without the heaviness of a border.

```css
.image-outline {
  outline: 1px solid rgba(0, 0, 0, 0.1);
  outline-offset: -1px;
}

.dark .image-outline {
  outline-color: rgba(255, 255, 255, 0.1);
}
```

The `outline-offset: -1px` pulls the outline inward so it sits on top of the image edge rather than outside it. This prevents the outline from adding to the element's visual size.

**When to use it:**
- Image galleries and grids
- Avatars and profile photos
- Card thumbnails
- Any image where the edge blends into the page background

**When to skip it:**
- Images with naturally dark/contrasting edges
- Full-bleed hero images
- Images already inside a card with [[shadows-over-borders]]

This is the same philosophy as [[shadows-over-borders]] — using transparency-based depth cues that adapt to any background. Where shadows add lift, outlines add containment. Both contribute to the considered feel described in [[design-taste]].
