---
description: "Drag gestures with snap points, progressive action reveal, elastic constraints, and momentum control. Practical patterns for swipe-to-action rows and dismissible cards."
title: Drag Interactions
---

# Drag Interactions

This goes deeper than the basic drag gesture in [[gestures]]. Drag interactions involve snap points, progressive reveal, elastic boundaries, and momentum control.

## Structure

An outer container with `overflow-clip` (clips but prevents scrolling) wrapping a content div that handles the gesture.

## Drag Configuration

```jsx
<motion.div
  drag="x"
  dragConstraints={{ left: -116, right: 116 }}
  dragElastic={0.05}
  dragMomentum={false}
  style={{ x }}
  onDragEnd={handleDragEnd}
/>
```

**dragConstraints** — boundaries of the draggable area. Limits how far the element can travel.

**dragElastic** — resistance past boundaries. Lower values (0.05) add minimal overshoot. Higher values allow more stretch before snapping back.

**dragMomentum** — set to `false` for swipe actions. You want the row to stop where you decide, not where velocity decides. This makes interactions feel consistent.

## Snap Points

When drag ends, snap to the nearest position based on distance from center:

```jsx
const SNAP_POINTS = { LEFT: -116, CENTER: 0, RIGHT: 116 };
const POSITION_THRESHOLD = 58;

const handleDragEnd = () => {
  const currentX = x.get();
  if (Math.abs(currentX) > POSITION_THRESHOLD) {
    animate(x, currentX > 0 ? SNAP_POINTS.RIGHT : SNAP_POINTS.LEFT, SPRING_CONFIG);
  } else {
    animate(x, SNAP_POINTS.CENTER, SPRING_CONFIG);
  }
};
```

The threshold is the commit point. Below it, the row snaps back. Above it, it opens.

## Progressive Reveal

Actions do not all appear at once. Compare the drag distance against thresholds to reveal actions progressively:

```jsx
<ActionButton isVisible={dragProgress > 44} label="Set reminder" />
<ActionButton isVisible={dragProgress > 88} label="Mark as unread" />
```

Each action button animates `opacity` and `scale` based on its `isVisible` prop. This creates the iOS-style layered reveal.

## Indicators

Render state indicators conditionally with [[animate-presence]] for exit animations. Add `transform-origin` to animate from the correct direction.

This pattern connects to the anticipation principle in [[animation-principles]] — the progressive reveal prepares the user for the available actions. The spring configurations used here are documented in [[spring-configs]].
