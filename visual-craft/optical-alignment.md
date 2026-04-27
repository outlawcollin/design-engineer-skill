---
description: "Geometric alignment is not always visual alignment. Icons, text, and shapes often need manual adjustment to look centered. Knowing when to break the grid is a mark of craft."
title: Optical Alignment
---

# Optical Alignment

Aligning items geometrically works most of the time, but there are instances where it looks off. When that happens, align optically instead.

## Buttons with Icons

When a button has both text and an icon, the side with the icon often needs smaller padding than the text side. Geometrically equal padding makes the button feel unbalanced because the icon has different visual weight than text.

## Icons

Many icon packs already account for optical alignment, but some shapes need manual adjustment. For icons, use `margin` or `padding` depending on the container. The ideal fix is in the SVG itself so no additional spacing is needed.

A play triangle, for example, needs to shift slightly right from geometric center to look centered. A star icon needs subtle adjustment too, though the change is more minor.

## The Takeaway

Sometimes it is fine, or even necessary, to break out of geometric alignment to make things feel visually balanced. Geometric alignment is not always the best way to align things.

This pairs with [[concentric-border-radius]]: both are about trusting your eyes over your grid. The solid drawing principle in [[animation-principles]] also applies here — making elements feel believable in their space requires optical, not just mathematical, precision.
