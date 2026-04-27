---
description: "Animating container width and height using a useMeasure hook (wrapping ResizeObserver) and Motion. The key pattern: measure the inner div, animate the outer div, never both on the same element."
title: Container Bounds Animation
---

# Container Bounds Animation

Width and height are not directly animatable — the browser cannot interpolate between a fixed value and "whatever the content needs." The solution is to measure content dimensions with a `ResizeObserver` hook and pass those values to Motion.

## The Pattern

Two divs: an outer div that you animate, and an inner div that you measure.

```jsx
function AnimatedContainer({ children }) {
  const [ref, bounds] = useMeasure();

  return (
    <motion.div animate={{ height: bounds.height }}>
      <div ref={ref}>{children}</div>
    </motion.div>
  );
}
```

Attach the `ref` from [[use-measure-hook]] to the inner div. `bounds.width` and `bounds.height` update whenever content changes. Pass those to Motion's `animate` prop on the outer div.

## Width Animation

Buttons that change their label (loading states, confirmation messages, multi-step forms). Without animated bounds, the button jumps between widths. With this pattern, it slides.

Check `bounds.width > 0` before animating to avoid an animation from 0 on initial render. The first frame should show the button at its natural size.

## Height Animation

This is where the pattern shines: expandable sections, accordions, FAQs, detail panels. When items are added or removed, the measured height changes and the animation follows.

## Gotchas

**Initial render**: `bounds` will be `0` before the first measurement. Guard with `bounds.height > 0 ? bounds.height : "auto"`.

**Measurement loop**: never measure and animate the same element. The ref goes on the inner div, `animate` goes on the outer div. Same element creates a loop: animation changes size, triggers measurement, triggers animation.

**Natural feel**: add a small delay to the transition so it feels like it is catching up to the content.

**Overuse**: this is a subtle effect. Use for buttons, accordions, dialogs — not for everything.

This pattern is used extensively in the [[animated-dialog]] where dialog height animates between steps. It connects to [[animate-presence]] because the `popLayout` mode works well with measured containers. See [[use-measure-hook]] for the hook implementation. Understanding [[will-change-performance]] helps here since height animation triggers layout recalculation.
