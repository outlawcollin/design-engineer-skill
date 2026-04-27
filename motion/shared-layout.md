---
description: "Motion's layoutId prop and the FLIP technique for animating elements between different positions, sizes, and states. Covers single elements, multiple elements, combining with AnimatePresence, and Radix integration."
title: Shared Layout Animations
---

# Shared Layout Animations

Shared layout animations let you animate between different elements with a single prop. When two elements share a `layoutId`, Motion animates between their positions, sizes, and styles automatically.

Under the hood, this uses the FLIP technique: First, Last, Inverse, Play. The browser records the element's position before and after the state change, then plays the inverse animation so it appears to travel between states.

## Single Element

Turn an element into a `motion` component and add `layoutId`:

```jsx
<motion.div
  className="size-16 rounded-full bg-gray-1200"
  layoutId="circle"
/>
```

In a tab interface, render the same circle in different positions based on the active tab. You are not manipulating the component — you render different components for each state with the same `layoutId` and Motion handles the interpolation.

## Multiple Elements

Animate between as many elements as needed. Each must have a unique `layoutId` within its group. This powers tab indicators, navigation highlights, and any morphing UI element.

## Combining with AnimatePresence

When using both `AnimatePresence` and shared layout animations, keep components with `layoutId` outside of `AnimatePresence`. If they are inside, `initial` and `exit` animations trigger while layout animation is running, which looks bad — especially with opacity animations.

```jsx
<motion.div layoutId="card" /* outside AnimatePresence */ />
<AnimatePresence mode="popLayout">
  <motion.div key={activeTab} /* content inside */ />
</AnimatePresence>
```

## With Radix Primitives

Shared layout animations pair naturally with Radix Dialog primitives. Two separate components (a card and a dialog) share a `layoutId`, and Motion animates between them when the dialog opens. This is used in the [[animated-dialog]] and [[collection-preview]] patterns.

## Tab Indicators

A common pattern: instead of filling a tab's background, add an absolutely positioned container with `inset-0` and animate it with `layoutId`:

```jsx
{activeTab === tab && (
  <motion.div
    initial={false}
    layoutId="tab-indicator"
    transition={{ type: "spring", duration: 0.4, bounce: 0 }}
  />
)}
```

This creates the morphing tab effect where the highlight slides between tabs. It is a direct implementation of the fluidity pillar in [[design-taste]].

## CSS Alternative

The View Transitions API in [[pseudo-elements]] provides a CSS-native alternative using `view-transition-name`. For simple cases it requires no JavaScript. For complex choreography, Motion's `layoutId` remains more flexible.
