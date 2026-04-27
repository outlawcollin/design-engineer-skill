---
description: "Motion's AnimatePresence component for animating elements that leave the DOM. Covers presence state reading, manual exit control, nested exit propagation, and the three modes: sync, wait, popLayout."
title: Animate Presence
---

# Animate Presence

When an element leaves the DOM, it is gone — there is no way to animate something that no longer exists. Motion's `AnimatePresence` fixes this by keeping departing elements mounted long enough to animate out, then removing them.

Basic usage: wrap conditional content, define `initial`, `animate`, and `exit` states. The component handles the rest. The interesting part is what happens when basic entry/exit is not enough.

## Reading Presence State

The `useIsPresent` hook tells a component whether it is exiting. Returns `true` while mounted normally, `false` during the exit animation.

Use it to disable buttons while a component exits, switch visual states on unmount, or trigger cleanup when departure begins. The hook must be called from a child of `AnimatePresence` — you cannot inline it in the parent where you conditionally render.

```jsx
function Card() {
  const isPresent = useIsPresent();
  return (
    <motion.div
      initial={{ opacity: 0, scale: 0.9 }}
      animate={{ opacity: 1, scale: 1 }}
      exit={{ opacity: 0, scale: 0.9 }}
      transition={{ duration: 0.4, ease: [0.19, 1, 0.22, 1] }}
    >
      {isPresent ? "Present" : "Exiting..."}
    </motion.div>
  );
}
```

## Manual Exit Control

`usePresence` returns both the presence state and a `safeToRemove` callback. The component stays mounted until you call it. The exit animation starts immediately and async work runs in parallel. When both finish, the element unmounts.

Use this to save draft content before a modal closes, wait for a network request, or hand control to GSAP for complex animation sequences.

## Nested Exits

When a parent `AnimatePresence` removes children, nested exit animations do not fire by default — the parent wins. The `propagate` prop enables both: removing the parent triggers exit animations on both parent and children. Without it, children vanish instantly.

This level of detail separates people who care about interaction quality from those who don't. It connects directly to the staging principle in [[animation-principles]] and the fluidity pillar of [[design-taste]].

## Modes

The `mode` prop controls timing between entering and exiting elements:

**sync** — entering and exiting elements animate simultaneously. Useful for crossfades. Both elements are visible at the same time, so handle layout accordingly.

**wait** — the exiting element finishes before the entering one starts. More elegant but nearly doubles the perceived duration. Adjust individual durations to compensate.

**popLayout** — removes exiting elements from document flow immediately, making them absolutely positioned. Surrounding content reflows. Use for list reordering, morphing layouts, and any case where layout shifts are unacceptable. This is the most commonly useful mode and pairs well with [[container-bounds]] for animated height.

Direct children of `AnimatePresence` must have a unique `key`. This is used in [[icon-transitions]] for swapping icons and in the [[animated-dialog]] pattern for stepping through dialog states.

## CSS Alternative

CSS now has `@starting-style` for native exit animations. Simple transitions no longer need JavaScript. But the patterns here — presence state reading, manual exit control, coordinated nested exits — require `AnimatePresence`. See [[pseudo-elements]] for the CSS-native direction.
