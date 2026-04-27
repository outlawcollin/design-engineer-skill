---
description: "Map of content for motion: animation techniques, gesture handling, enter/exit choreography, layout animations, and interaction patterns using Motion (formerly Framer Motion)."
title: Motion
---

# Motion

Motion is where design engineering becomes tangible. This cluster covers the techniques for making interfaces move with intention, from basic gesture handling to complex choreographed transitions.

The primary tool is [Motion](https://motion.dev/) (the React animation library), though the concepts apply broadly.

## Interaction Foundations

- [[gestures]] — the six gesture types in Motion: hover, tap, drag, pan, focus, and inView. Each has a `while-` prop for declarative animation. Understanding gestures is prerequisite to [[drag-interactions]] which goes deeper on drag specifically. Performance connects to [[will-change-performance]] since gesture animations benefit from GPU compositing.

## Enter/Exit Choreography

- [[animate-presence]] — Motion's solution for animating elements that leave the DOM. Covers presence state reading with `useIsPresent`, manual exit control with `usePresence` and `safeToRemove`, nested exit propagation, and the three modes: sync, wait, and popLayout. This is the most-used Motion feature and connects to [[icon-transitions]] and the [[animated-dialog]] pattern.

- [[staggered-entries]] — breaking entering content into individually animated chunks with staggered delays. Covers section-level stagger, word-by-word text splitting, and the CSS custom property pattern (`--stagger`, `--delay`). Applies the staging principle from [[animation-principles]].

- [[exit-animations]] — exits should be subtler than entrances. Exiting elements are being dismissed — they should leave quietly with reduced travel distance and shorter duration. Connects to [[animate-presence]] for implementation.

## Animation Quality

- [[interruptible-animations]] — CSS transitions retarget mid-flight while keyframe animations run on fixed timelines. Choosing the right one prevents interfaces from feeling broken when users change intent mid-interaction. Rule of thumb: transitions for reversible interactions, keyframes for staged sequences like [[staggered-entries]].

## Layout Animation

- [[shared-layout]] — the `layoutId` prop and the FLIP technique. When two elements share a `layoutId`, Motion animates between their positions automatically. This powers tab indicators, card-to-detail expansions, and any morph transition. Connects to [[collection-preview]] pattern and the fluidity pillar of [[design-taste]].

- [[container-bounds]] — animating width and height requires measuring content with a `useMeasure` hook (wrapping `ResizeObserver`), then passing measured values to Motion's `animate` prop. The key rule: measure the inner div, animate the outer div, never both on the same element. Used extensively in [[animated-dialog]].

## Gesture Deep-Dives

- [[drag-interactions]] — drag gestures with snap points, progressive reveal, elastic constraints, and momentum control. Builds on [[gestures]] with practical patterns like swipe-to-action rows with configurable thresholds.

## Icon Animation

- [[icon-transitions]] — animating opacity, scale, and blur when icons swap contextually using `AnimatePresence` with `popLayout` mode. A focused technique that makes any icon state change feel intentional. Connects to [[animate-presence]].

- [[icon-morphing]] — a universal icon primitive where every icon uses exactly three SVG lines. Icons in the same rotation group rotate between states; cross-group icons morph coordinates. Connects to the follow-through principle in [[animation-principles]].
