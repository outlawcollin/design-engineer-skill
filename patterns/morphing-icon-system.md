---
description: "A universal icon component where any of 21 icons morphs into any other through SVG line interpolation and rotation groups. Full implementation reference for the constraint-driven approach."
title: Morphing Icon System
---

# Morphing Icon System

A component where 21 icons can each morph into any other. Not through crossfades or opacity tricks, but through actual transformation of the underlying SVG shapes. See [[icon-morphing]] for the technique and design philosophy.

## Architecture

Every icon is represented by exactly three SVG lines. The component stores line coordinates for each icon and Motion tweens between them on state change.

**Collapsed lines**: icons that need fewer than three lines collapse extras to invisible center points:
```
{ x1: 7, y1: 7, x2: 7, y2: 7 }  // with opacity: 0
```

## The 21 Icons

Menu, cross, plus, minus, equals, asterisk, more, check, play, pause, download, upload, external, four arrow directions, four chevron directions. Each defined as three line coordinate sets.

## Rotation Groups

Icons in the same group share coordinates and differ only by rotation:

**Arrows** — four directions, 90 degrees apart
**Chevrons** — same shape as arrows without the shaft, 90 degrees apart
**Plus / Cross** — the same perpendicular lines, 45 degrees apart

Within a group, the component applies CSS `rotate()`. Between groups, line coordinates interpolate through space. This distinction is critical: coordinate morphing on same-shape icons creates warping artifacts, while rotation creates natural arcs (connecting to the arcs principle in [[animation-principles]]).

## Cross-Group Morphs

When transitioning between different groups (arrow to check, menu to plus), Motion interpolates each line's x1, y1, x2, y2 coordinates independently. These transitions feel the most magical because you watch shapes genuinely transform.

## Building a Sequencer

During development, build a test sequencer to click through icon transitions and identify which sequences feel wrong. Point to specific transitions and describe what feels off. The iterative feedback loop — watch, notice, describe, adjust — is the actual workflow.

## Limitations

With hundreds of possible icon pairs, not every transition takes the ideal path. Some morphs have awkward intermediate states, some rotations overshoot. These are fixable with more iteration. The agent cannot tell when something looks wrong — the insight about rotation vs morphing, for example, requires human visual judgment.

This pattern demonstrates constraint-driven design: fixing the structure creates emergent flexibility. It connects to [[icon-transitions]] (the simpler swap approach) and the follow-through principle in [[animation-principles]] (springs make the transitions feel alive). The spring values used are in [[spring-configs]].
