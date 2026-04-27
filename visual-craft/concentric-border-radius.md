---
description: "When nesting elements, the outer border radius must equal the inner radius plus the padding. Mismatched curvature is one of the most visible tells of an unpolished interface."
title: Concentric Border Radius
---

# Concentric Border Radius

Concentric offset creates a balanced visual look when nesting elements. Humans are sensitive to mismatched curvature because our visual system is tuned to detect irregularities in edges and contours.

## The Formula

The outer radius of an element equals the inner radius plus the padding:

```
outer radius = inner radius + padding
```

If the inner border radius is `12px` and the padding is `8px`, the outer border radius should be `20px`. This formula is unnecessary when `border-radius` is `0` or `9999px` (full), because the radii look balanced regardless of padding.

## Physical World Origin

This principle comes from industrial design. Watch cases, for example: the radii between the crystal and the case, between the inside and outside of the case, and between the edge and the bezel are precisely calculated. Look around your surroundings — objects that feel well-crafted follow this approach.

## In Practice

A surprising number of apps and interfaces mismatch border radii. Applying this consistently makes interfaces feel noticeably better. Apple added `.concentric` to SwiftUI. Sketch added auto border radius. Both make it easier to apply than manual calculation.

This is not a one-size-fits-all solution — there will be edge cases where it is not possible. But default to it whenever nesting rounded elements.

This technique pairs with [[optical-alignment]]: both are about trusting visual perception over mathematical precision. It also connects to the solid drawing principle in [[animation-principles]], which emphasizes making objects feel believable in their space.
