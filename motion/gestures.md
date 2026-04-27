---
description: "The six gesture types in Motion: hover, tap, drag, pan, focus, and inView. Each has a declarative while- prop for animation. Covers spring vs CSS performance, accessibility, and when to use each gesture."
title: Gestures
---

# Gestures

Gestures make elements feel alive. The user performs an action and the interface responds. Motion extends React's event system with six gesture types: hover, tap, drag, pan, focus, and inView.

To use gestures, wrap elements in `motion` components. Each gesture has a `while-` prop for declarative animation (except pan, which uses event handlers).

## Hover

`whileHover` detects pointer enter and leave. Motion's advantage over CSS is easy spring animations — in certain scenarios springs create more natural-looking motion than CSS transitions.

```jsx
<motion.div
  whileHover={{ rotate: 180 }}
  transition={{ type: "spring", duration: 0.8, bounce: 0 }}
/>
```

Performance: for `transform`, `clipPath`, and `filter` animations, CSS and Motion behave almost identically. Motion animations still run on the compositor thread. Sometimes Motion performs better because it handles independent transforms more efficiently. See [[will-change-performance]] for why.

## Tap

`whileTap` fires when a pointer presses and releases on the same element. Automatically cancels if the pointer moves too far, so it won't conflict with drags. Keyboard accessible: pressing Return triggers `onTapStart` and `whileTap`.

```jsx
<motion.div
  whileTap={{ scale: 0.8 }}
  transition={{ type: "spring", duration: 0.5, bounce: 0 }}
/>
```

## Drag

The `drag` prop applies pointer movement directly to a component. Add `whileDrag` for animation during drag. Use `dragConstraints` to limit the draggable area. For deeper drag patterns, see [[drag-interactions]].

```jsx
<motion.div
  whileDrag={{ scale: 0.8 }}
  drag
  dragConstraints={constraintsRef}
/>
```

## Pan

Pan recognizes when a pointer moves more than 3 pixels while pressed. No `while-` prop — use `onPan`, `onPanStart`, `onPanEnd` handlers. Good for sliders, scrollable areas, and custom controls. Springs over regular easing make pan interactions feel more natural. See [[spring-configs]].

## Focus

`whileFocus` fires when an element gains or loses focus, matching CSS `:focus-visible` behavior. Adds visual feedback for keyboard navigation. Keep focus animations subtle — complex motion can feel disorienting when navigating by keyboard.

## InView

`whileInView` triggers when an element enters or exits the viewport. Pair with `initial` for scroll-based reveals. Configure the viewport root and threshold with the `viewport` prop.

```jsx
<motion.div
  initial={{ filter: "blur(8px)" }}
  whileInView={{ scale: 1.1, rotate: 45, filter: "blur(0px)" }}
  viewport={{ root: scrollRef, amount: 0.5 }}
/>
```

Each gesture connects to specific [[animation-principles]]: hover and tap use squash and stretch, inView uses staging, drag uses follow-through. The delight pillar of [[design-taste]] guides which gestures deserve spring animations versus simple easing.
