---
description: "An expandable image collection with stacked hover state, spring-driven proximity scaling, shared layout transitions between collapsed and expanded views, and mouse-tracking offset calculations."
title: Collection Preview
---

# Collection Preview

An image collection that transitions between a collapsed stack and an expanded row. The collapsed state fans images on hover. The expanded state scales images based on cursor proximity. Built with [[shared-layout]] for the state transition and [[gestures]] for interaction.

## Collapsed State

Images are absolutely positioned and stacked. Each has custom rotation, position, and z-index variants for hover:

```jsx
const imageVariants = [
  { hover: { rotate: -24, x: -32, y: -20, zIndex: 3 }, rest: { rotate: -12, zIndex: 3 } },
  { hover: { rotate: 24, x: 28, y: -16, zIndex: 4 }, rest: { rotate: 12, zIndex: 4 } },
  // ...
];
```

Each image has a unique `layoutId` for the cross-state animation. The collection avatar is separate because it behaves differently in the expanded state. Text elements use `whitespace-nowrap` to prevent line breaks during animation.

## Expanded State

Images move to a flex container. The key interaction is proximity-based scaling: images near the cursor grow, images far away are pushed outward.

**Distance calculation**: for each image, compute the distance from cursor to image center using `useTransform`:

```jsx
const distance = useTransform(() => {
  const bounds = ref.current
    ? { x: ref.current.offsetLeft, width: ref.current.offsetWidth }
    : { x: 0, width: 0 };
  return (mouseLeft?.get() ?? 0) - bounds.x - bounds.width / 2;
});
```

**Scale**: interpolate from 1 (far) to SCALE (directly under cursor) based on distance:

```jsx
const scale = useTransform(distance, [-DISTANCE, 0, DISTANCE], [1, SCALE, 1]);
```

**Offset**: push images away from the cursor. `Math.sign(currentDistance)` ensures images push in the correct direction. Returns 0 when no mouse interaction.

**Springs**: `useSpring` smooths the raw scale and position values. See [[spring-configs]] for the parameters.

## Magic Numbers

```jsx
const SCALE = 1.5;      // max scale on hover
const DISTANCE = 100;   // influence radius in pixels
const NUDGE = 24;       // push distance in pixels
const SPRING_CONFIG = { mass: 0.1, stiffness: 300, damping: 20 };
```

These control the feel. Adjust SCALE for how dramatic the hover is, DISTANCE for how wide the influence, NUDGE for how much surrounding images shift.

## Assembly

Everything wrapped in `MotionConfig` for shared transition defaults, `AnimatePresence` with `popLayout` for the state switch, and keyed containers for collapsed/expanded:

```jsx
<MotionConfig transition={{ type: "spring", duration: 0.5, bounce: 0 }}>
  <AnimatePresence mode="popLayout" initial={false}>
    {!isExpanded ? <CollapsedState key="collapsed" /> : <ExpandedState key="expanded" />}
  </AnimatePresence>
</MotionConfig>
```

This pattern combines [[shared-layout]] for the macro transition, [[gestures]] for micro interactions, [[animate-presence]] for state choreography, and the follow-through principle from [[animation-principles]] for spring-driven movement.
