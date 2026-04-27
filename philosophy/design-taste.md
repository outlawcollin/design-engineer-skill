---
description: "The three ordered pillars of design taste: simplicity through gradual revelation, fluidity through seamless transitions, and delight through selective emphasis. A framework for making interfaces feel crafted and intentional."
title: Design Taste
---

# Design Taste

Taste is the difference between an interface that works and one that someone uses and thinks "whoever made this actually cares." It is built on three pillars, applied in strict order. You cannot have delight without fluidity, and you cannot have fluidity without simplicity.

## Simplicity — Gradual Revelation

Show only what matters right now. The interface should feel like walking through rooms, where you glimpse what's next before you arrive.

One primary action per view. Two equally weighted CTAs is a failure. Progressive disclosure over feature dumps: layered trays, step-by-step flows, expandable sections. Never show a 12-field form when 3 steps of 4 fields works.

Context-preserving overlays over full-page navigations. Sheets and modals that overlay the current context keep users oriented. Stacked layers must be visibly different heights so progression is clear. Every overlay needs a title and dismiss action.

**Self-check**: Can the user tell within 1 second what to do next? If not, simplify.

## Fluidity — Seamless Transitions

Treat your app as a space with unbreakable physical rules. Every element moves from somewhere to somewhere. No instant show/hide, ever.

If an element exists in both State A and State B, it must visually travel between them using [[shared-layout]] techniques. Never unmount and remount — morph. Directional consistency matters: navigate right and content enters from right, go back and content enters from left. This builds spatial memory.

When button labels change, animate the transition. Identify shared letter sequences and keep them fixed while the rest morphs. Persistent elements stay put: a header that persists across a transition must not fade out and back in.

The golden easing curve is `cubic-bezier(0.16, 1, 0.3, 1)` — fast start, gentle settle. Use for all entrances and morphs. Use `ease-in` for exits only. Never use linear. See [[easing-reference]] for the full timing table.

**Self-check**: Record your screen at 0.5x speed. Can you follow every element's journey? Anything that teleports needs a transition.

## Delight — Selective Emphasis

The Delight-Impact Curve: the less frequently a feature is used, the more delightful it should be. Daily actions need efficiency with subtle touches. Rare moments deserve theatrical ones.

Polish everything equally. The settings page, the empty state, the error screen all receive the same care as the hero section. One unpolished corner makes the whole feel unpolished.

Celebrate completions with animation and [[sound-design]], not just a green checkmark. Make destructive actions satisfying. Animate numbers when they change. Empty states are first impressions, not afterthoughts.

**Self-check**: Show your UI to someone for 30 seconds. Do they smile? If not, add delight. Do they look annoyed? You over-delighted a high-frequency interaction.

## Anti-Patterns

Static tab switches with no directional slide. Modals that pop from nowhere instead of growing from their trigger. Skeleton screens that don't match the real layout. Redundant animations on persistent elements. Linear easing. "No items" empty text with nothing else. Toasts for important outcomes that deserve inline, contextual feedback. Forms that are just stacked inputs instead of stepped flows.

## The Taste Checklist

Run before considering any UI done. See each pillar's self-check above, and verify: no generic aesthetics, intentional typography pairing, a dominant color with sharp accents, generous consistent spacing, and an interface that feels like a physical space. See [[animation-principles]] for the motion foundations and [[easing-reference]] for timing values.
