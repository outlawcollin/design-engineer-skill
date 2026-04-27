---
description: "In light mode, a layered box-shadow creates more depth and adaptability than a flat border. Shadows use transparency and adapt to any background, where solid borders can clash."
title: Shadows Over Borders
---

# Shadows Over Borders

Instead of using a border in light mode, use a subtle layered `box-shadow` that adds depth to the element.

## The Technique

The shadow is comprised of three layers:

```css
.border-shadow {
  box-shadow:
    0px 0px 0px 1px rgba(0, 0, 0, 0.06),
    0px 1px 2px -1px rgba(0, 0, 0, 0.06),
    0px 2px 4px 0px rgba(0, 0, 0, 0.04);
}
```

The first layer (`0px 0px 0px 1px`) replaces the border. The second and third add subtle depth. For hover states, use the same structure with slightly darker values:

```css
.border-shadow:hover {
  box-shadow:
    0px 0px 0px 1px rgba(0, 0, 0, 0.08),
    0px 1px 2px -1px rgba(0, 0, 0, 0.08),
    0px 2px 4px 0px rgba(0, 0, 0, 0.06);
}
```

Transition between states with `transition-property: color, box-shadow`.

## Why Shadows Win

Shadows adapt to any background because they use transparency. This matters when using images or multiple colors as backgrounds — solid borders can clash or disappear. Shadows remain consistent.

These exact values are extracted in [[shadow-tokens]] for quick reuse. This technique connects to the solid drawing principle in [[animation-principles]]: shadows create the illusion of depth and hierarchy that flat borders cannot.
