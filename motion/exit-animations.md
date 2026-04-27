---
description: "Exit animations should be subtler than entrances. Covers the asymmetry between enter and exit motion, with specific techniques for reducing exit intensity."
title: Exit Animations
---

# Exit Animations

Enter and exit animations should not be symmetrical. Entering elements need to announce themselves — they carry new information. Exiting elements are being dismissed — they should leave quietly.

## The Problem with Symmetric Exits

A common pattern is mirroring the enter animation on exit:

```jsx
<motion.div
  initial={{ opacity: 0, y: "calc(-100% - 4px)", filter: "blur(4px)" }}
  animate={{ opacity: 1, y: 0, filter: "blur(0px)" }}
  exit={{ opacity: 0, y: "calc(-100% - 4px)", filter: "blur(4px)" }}
  transition={{ type: "spring", duration: 0.45, bounce: 0 }}
/>
```

The full `calc(-100% - 4px)` exit distance matches the entrance, making the departure just as visually demanding as the arrival. This fights for attention when the user has already moved on.

## Subtle Exits

Replace the full travel distance with a small fixed value:

```jsx
exit={{
  opacity: 0,
  y: "-12px",
  filter: "blur(4px)",
}}
```

The `-12px` gives directional hint — the element is leaving upward — without the full slide. The `opacity` and `blur` do most of the work. The motion is felt more than seen.

## Guidelines

- **Keep some motion** — don't just fade to zero. A small `y` or `scale` shift preserves directional context
- **Reduce distance** — `8-16px` fixed value instead of percentage-based travel
- **Shorten duration** — exits can be 20-30% faster than entrances
- **Skip blur on fast exits** — if the exit is under 150ms, blur may not register and just costs performance

## When Symmetric Exits Work

Full symmetric exits are appropriate when the enter and exit represent equal actions — like a toggle switching between two equal states. The asymmetry rule applies when one direction is more important than the other (most cases).

This connects to the staging principle in [[animation-principles]] — direct attention where it matters. Exits that demand equal attention violate the fluidity pillar of [[design-taste]] by creating unnecessary visual noise. See [[animate-presence]] for the implementation mechanics.
