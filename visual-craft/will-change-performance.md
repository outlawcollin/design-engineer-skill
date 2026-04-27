---
description: "The will-change CSS property hints to the browser that specific properties will animate, enabling GPU layer promotion to prevent first-frame stutter. Covers the layout-paint-compose pipeline."
title: Will-Change Performance
---

# Will-Change Performance

`will-change` is a hint to the browser: "I'm about to animate these properties, please get ready." Browsers may respond by promoting the element to its own GPU compositing layer, pre-allocating memory, or doing nothing if they decide the hint is not worth it.

## The Rendering Pipeline

Browsers render in three steps:

**Layout** — figures out how big every box is and where it sits. CPU work.

**Paint** — fills boxes with pixels: colors, borders, shadows, images. CPU work plus memory for painted bits.

**Compose** — painted layers go to the GPU, which stacks them together for the final frame. GPU-heavy.

If an animation touches only compositor-friendly properties (`transform`, `opacity`), the browser can skip layout and paint entirely and let the GPU handle everything. This is why these properties are cheap to animate and `width`/`height` are expensive.

## What will-change Does

Without the hint, the browser promotes an element to its own layer only when animation starts. That one-time promotion can cause a tiny stutter in the first frames.

```css
.animated-button {
  will-change: transform;
  transform: translateX(0px);
  transition: transform 0.3s;
}
```

With `will-change`, the browser pre-promotes the element when idle, so the animation is smooth from frame one.

## Usage Rules

Creating and maintaining extra layers costs memory. `will-change` should be used intentionally:

Specify exactly what will change. Use `will-change: transform, opacity` not `will-change: all`. Only apply to elements that will actually animate.

The properties that make a real difference: `transform`, `opacity`, `filter` (blur, brightness), `clip-path`, `mask`. Also `scroll-position` for scroll-only animations and `contents` for containers with frequently updating children.

Properties like `top`, `background`, `border` are legal to write but don't actually speed anything up — they just ask the browser to reserve extra memory for no real gain.

## Connection to Motion

Every technique in [[motion]] benefits from understanding this pipeline. [[gestures]] trigger animations that should run on the compositor thread. [[animate-presence]] exit animations should use `transform` and `opacity` to avoid layout recalculation. The [[container-bounds]] pattern explicitly animates `height` (expensive) — understanding why helps you add appropriate `will-change` hints and keep `overflow: hidden` to contain repaints.

Safari in particular benefits from `will-change` — the difference between with and without is very noticeable for transform animations.
