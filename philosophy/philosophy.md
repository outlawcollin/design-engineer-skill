---
description: "Map of content for design philosophy: the foundational thinking about why interfaces should feel a certain way, covering taste, animation principles, and sound design."
title: Philosophy
---

# Philosophy

Design engineering starts with intent. Before writing CSS or choosing an animation library, you need a framework for what "good" means and why.

This cluster covers the philosophical foundations:

- [[design-taste]] is the overarching framework, built on three ordered pillars: simplicity first, then fluidity, then delight. You cannot have delight without fluidity, and you cannot have fluidity without simplicity. This node connects heavily to [[motion]] because fluidity is fundamentally about how things move, and to [[sound-design]] because audio is a delight multiplier.

- [[animation-principles]] adapts Disney's 12 principles for UI. These are not arbitrary rules but observations about how humans perceive movement. Every technique in [[motion]] traces back to at least one of these principles: [[animate-presence]] uses staging and anticipation, [[shared-layout]] uses follow-through, [[gestures]] use squash and stretch.

- [[sound-design]] makes the case that the web's silence is a historical accident, not a design principle. Audio feedback processed 10x faster than visual feedback makes interactions feel more responsive. This connects to the delight pillar of [[design-taste]] and to the secondary action principle in [[animation-principles]].

These three nodes form the "why" layer. Everything else in the graph is "how."
