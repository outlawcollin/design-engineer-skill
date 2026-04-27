---
description: "Map of content for visual craft: CSS techniques and visual design principles for polish, depth, color, alignment, and rendering performance."
title: Visual Craft
---

# Visual Craft

Visual craft is the collection of techniques that make interfaces feel considered at the pixel level. These are not animations or interactions but the static visual qualities that communicate care.

- [[concentric-border-radius]] — when nesting elements, the outer radius must equal the inner radius plus the padding. Mismatched curvature is one of the most common tells of an unpolished interface. This principle comes from industrial design and connects to the broader idea of [[optical-alignment]].

- [[optical-alignment]] — geometric alignment is not always visual alignment. Icons, text, and shapes often need manual adjustment to look centered. This is the companion to [[concentric-border-radius]]: both are about trusting your eyes over your grid.

- [[shadows-over-borders]] — in light mode, a layered box-shadow creates more depth than a flat border. Shadows adapt to any background because they use transparency, where solid borders can clash. This technique connects to the solid drawing principle in [[animation-principles]].

- [[oklch-color]] — the OKLCH color model produces perceptually uniform palettes. Change only the hue and the lightness stays consistent, unlike HSL where brightness drifts unpredictably. Essential for creating systematic color scales and vibrant gradients without muddy midpoints.

- [[pseudo-elements]] — modern CSS pseudo-elements go beyond `::before` and `::after`. View transitions, scroll markers, and native dialog styling hooks reduce JavaScript dependency. The `::view-transition-group` pseudo-element connects directly to [[shared-layout]] as a CSS-native alternative.

- [[text-rendering]] — two text polish techniques: `text-wrap: balance` for preventing orphaned words, and `-webkit-font-smoothing: antialiased` for crisper rendering on macOS. Small details that compound into a feeling of care. Connects to [[optical-alignment]] as part of trusting your eyes over defaults.

- [[tabular-numbers]] — `font-variant-numeric: tabular-nums` gives digits equal width, preventing layout shift when numbers update in counters, timers, and prices. A close relative of [[optical-alignment]] — both prevent visual jitter.

- [[image-outlines]] — a `1px` transparent outline with `outline-offset: -1px` adds subtle depth to images. The containment counterpart to [[shadows-over-borders]] — where shadows add lift, outlines add boundary.

- [[will-change-performance]] — a GPU compositing hint that prevents first-frame stutter in animations. Understanding the layout-paint-compose pipeline explains why `transform` and `opacity` are cheap to animate while `width` and `height` are expensive. This connects to every node in [[motion]].
