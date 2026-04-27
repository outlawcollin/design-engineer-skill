---
description: "A universal icon primitive where every icon uses exactly three SVG lines. Same-group icons rotate between states; cross-group icons morph coordinates. Constraint-driven design creating emergent flexibility."
title: Icon Morphing
---

# Icon Morphing

Instead of crossfading or swapping icons, transform the underlying shapes. The hamburger menu rotates into an X. The play button becomes pause. These transitions feel considered in a way that static changes do not.

## The Constraint

Every icon uses exactly three SVG lines. Icons that need fewer collapse the extras to invisible center points (`{ x1: 7, y1: 7, x2: 7, y2: 7 }` with `opacity: 0`). This means any icon can morph into any other since they share the same underlying structure.

## Natural Mappings

Some icons map naturally: menu is three horizontal bars, plus is vertical and horizontal with the third collapsed, cross is plus rotated 45 degrees. Others require creativity: the checkmark uses two lines for its legs and collapses the third, play uses three lines forming a triangle with shared endpoints.

## Rotation Groups

Icons that are the same shape at different rotations should rotate, not morph coordinates. Arrow-right to arrow-down is a 90-degree rotation — morphing the coordinates makes lines bend and warp unnaturally.

Rotation groups: arrows rotate in 90-degree increments, chevrons the same, plus and cross are 45 degrees apart. When transitioning within a group, the component rotates. Between groups, lines interpolate through coordinate space.

## Cross-Group Morphs

These are the transitions that feel most magical — watching shapes genuinely transform into other shapes. Motion handles the tweening automatically. Arrow-to-check is particularly satisfying.

## The Design Approach

This demonstrates constraint-driven design: fixing the structure (three lines per icon) creates emergent flexibility. The constraint is what makes universal morphing possible.

When building something similar, the process is iterative: play with the result, notice what feels wrong, describe it, adjust. The insight about rotation vs coordinate morphing, for example, only becomes obvious when you watch the transition.

## Prompt for Building

```
Build an icon component where any icon can smoothly morph into any other.
Every icon should use exactly three SVG lines. Icons that need fewer lines
collapse the extras to invisible center points. For icons that are the same
shape at different rotations (like arrows), use rotation instead of
coordinate morphing.
```

This connects to the follow-through and arcs principles in [[animation-principles]] — rotation creates natural arcs where coordinate morphing creates jarring straight-line interpolation. For simpler icon state changes (opacity/scale swap rather than shape morphing), see [[icon-transitions]]. The full component implementation is in [[morphing-icon-system]].
