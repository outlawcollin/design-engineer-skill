---
description: "Map of content for component patterns: full implementations that combine multiple techniques from philosophy, visual craft, and motion into real, production-quality UI components."
title: Patterns
---

# Patterns

Patterns are where everything converges. Each node in this cluster is a complete component implementation that pulls from multiple areas of the graph. They serve as both learning material and implementation references.

- [[animated-dialog]] — a multi-step sign-in dialog built on Radix primitives with animated height using [[container-bounds]], content transitions using [[animate-presence]] with `popLayout` mode, morphing tab indicators using [[shared-layout]], and a rotating conic-gradient progress animation. Demonstrates how [[design-taste]]'s simplicity pillar (progressive disclosure through dialog steps) combines with fluidity (every state change animates).

- [[collection-preview]] — an expandable image collection with a collapsed hover state (stacked images with rotation variants) and an expanded state with proximity-based scale and offset using `useTransform`, `useSpring`, and mouse tracking. Combines [[shared-layout]] for the collapse/expand transition with [[gestures]] for the hover interaction. The spring configurations connect to [[reference]].

- [[morphing-icon-system]] — a universal icon component where any icon morphs into any other through SVG line interpolation. Uses rotation groups for same-shape icons (arrows, chevrons, plus/cross) and coordinate morphing for cross-group transitions. Demonstrates the constraint-driven design approach: fixing the structure (three lines per icon) creates emergent flexibility. Connects to [[icon-morphing]] for the technique and [[animation-principles]] for follow-through and arcs.

Each pattern includes inline code and links to the relevant [[reference]] files for reusable hooks and configurations.
