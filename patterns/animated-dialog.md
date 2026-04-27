---
description: "A multi-step sign-in dialog built on Radix primitives with animated height, content transitions using AnimatePresence, morphing tab indicators, and a rotating conic-gradient progress animation."
title: Animated Dialog
---

# Animated Dialog

A sign-in dialog with five states (default, wallet connection, email, phone, passkey) that transitions smoothly between them. Built on Radix Dialog primitives with Motion for animation.

## Animated Height

Animating `height` to `auto` does not work in CSS — the browser needs concrete start and end values. The solution uses [[container-bounds]]: wrap content in a measured div, pass the measured height to Motion.

```jsx
const [ref, bounds] = useMeasure({ offsetSize: true });

<Dialog>
  <DialogContent asChild>
    <motion.div
      animate={{ height: step === "default" ? 388 : bounds.height }}
      className="overflow-hidden will-change-transform"
    >
      <div ref={ref}>{content}</div>
    </motion.div>
  </DialogContent>
</Dialog>
```

The hardcoded default height (388) prevents a flash-from-zero on initial open. Purely using `bounds.height` would animate from 0. See [[use-measure-hook]] for the hook.

## Content Transitions

Each dialog state renders different content. Wrap in [[animate-presence]] with `popLayout` mode to stack content during transitions:

```jsx
<AnimatePresence mode="popLayout" initial={false}>
  <motion.div
    key={step}
    initial={{ opacity: 0, scale: 0.95 }}
    animate={{ opacity: 1, scale: 1 }}
    exit={{ opacity: 0, scale: 0.95 }}
    transition={{ type: "spring", bounce: 0, duration: 0.3 }}
  >
    {renderState()}
  </motion.div>
</AnimatePresence>
```

The `key` must be unique per state. `popLayout` removes the exiting content from flow so the entering content positions correctly.

## Morphing Tab Indicator

The default state has a tab component switching between sign-in methods. Instead of filling the active tab's background, use an absolutely positioned element with [[shared-layout]]:

```jsx
{activeTab === tab && (
  <motion.div
    initial={false}
    layoutId="tab-indicator"
    transition={{ type: "spring", duration: 0.4, bounce: 0 }}
  />
)}
```

The indicator slides between tabs rather than snapping. This is the fluidity pillar of [[design-taste]] in action.

## Progress Animation

The passkey state uses a rotating conic-gradient clipped by `overflow-hidden` to create an animated border:

```jsx
<motion.div
  className="absolute left-[-50%] top-[-50%] h-[200%] w-[200%]
    bg-[conic-gradient(from_0deg,transparent_0%,#4DAFFE_10%,#4DAFFE_25%,transparent_35%)]"
  animate={{ rotate: 360 }}
  transition={{ duration: 1.25, repeat: Infinity, ease: "linear", repeatType: "loop" }}
/>
```

The gradient element is oversized (200%) and centered, so rotation creates a smooth sweeping border effect inside the clipped container.

## Techniques Combined

This pattern demonstrates how [[container-bounds]], [[animate-presence]], and [[shared-layout]] compose together in a single component. The [[easing-reference]] and [[spring-configs]] provide the specific values used throughout.
