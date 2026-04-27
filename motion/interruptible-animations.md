---
description: "Why animations must be interruptible: CSS transitions retarget mid-flight while keyframe animations run on fixed timelines. Choosing the right one prevents interfaces from feeling broken."
title: Interruptible Animations
---

# Interruptible Animations

Users change their intent mid-interaction. They open a dropdown and immediately decide to close it. They hover a button, move away, hover again. If animations cannot be interrupted and redirected, the interface feels unresponsive — or broken.

## Transitions vs Keyframes

CSS transitions and keyframe animations handle interruption differently:

**Transitions** interpolate toward the latest target state. If the target changes mid-flight, the animation smoothly redirects. This makes them naturally interruptible.

```css
.dropdown {
  transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.dropdown.open {
  transform: translateY(0);
}

.dropdown.closed {
  transform: translateY(-12px);
}
```

Toggle the class at any point and the transition retargets gracefully.

**Keyframe animations** run on a fixed timeline. Once started, they play to completion regardless of state changes. Triggering a new animation before the current one finishes creates a hard jump.

```css
@keyframes slideIn {
  from { transform: translateY(-12px); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}

.dropdown.open {
  animation: slideIn 0.3s ease-out forwards;
}
```

If the user closes the dropdown before `slideIn` finishes, the exit animation starts from wherever the element happens to be — causing a visible snap.

## Rule of Thumb

- **Transitions** — interactions the user can reverse (toggles, hovers, dropdowns, tabs)
- **Keyframes** — staged sequences that run once (page load entrances, progress animations, [[staggered-entries]])

## Motion Library Context

Motion (Framer Motion) handles interruptibility automatically — its spring and tween animations retarget when props change. This is one of the key reasons to use it over raw CSS for interactive animations. But for simple hover states and toggles, CSS transitions are lighter and equally effective.

This connects to the anticipation and follow-through principles in [[animation-principles]] — an interrupted animation that redirects smoothly demonstrates the same physical believability as a well-timed ease curve. See [[easing-reference]] for the specific curves, and the fluidity pillar of [[design-taste]] for why interruptibility matters at the experience level.
