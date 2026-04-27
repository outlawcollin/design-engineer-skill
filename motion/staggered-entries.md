---
description: "Splitting entering content into individually animated chunks with staggered delays. Covers section-level stagger, word-by-word text splitting, and the CSS custom property pattern."
title: Staggered Entries
---

# Staggered Entries

Animating a single large block into view feels flat. Breaking the content into smaller chunks and staggering their entrance creates a cascade that draws the eye through the content in order — the staging principle from [[animation-principles]] applied to page sections.

## The Pattern

Each chunk animates with `opacity`, `translateY`, and optionally `blur`. A CSS custom property controls the stagger index:

```css
@keyframes enter {
  from {
    transform: translateY(8px);
    filter: blur(5px);
    opacity: 0;
  }
}

.animate-enter {
  animation: enter 800ms cubic-bezier(0.25, 0.46, 0.45, 0.94) both;
  animation-delay: calc(var(--delay, 0ms) * var(--stagger, 0));
}
```

```jsx
<div className="animate-enter" style={{ "--stagger": 1 }}>
  <Title />
</div>
<div className="animate-enter" style={{ "--stagger": 2 }}>
  <Description />
</div>
<div className="animate-enter" style={{ "--stagger": 3 }}>
  <Buttons />
</div>
```

A `100ms` delay between sections feels natural. Faster and the stagger disappears; slower and it drags.

## Word-by-Word Splitting

For hero text, split the title into individual spans — each word animated separately with a tighter delay:

```jsx
{title.split(" ").map((word, i) => (
  <span
    key={i}
    className="animate-enter"
    style={{ "--stagger": i, "--delay": "80ms", display: "inline-block" }}
  >
    {word}&nbsp;
  </span>
))}
```

`80ms` per word keeps the cascade feeling fluid without dragging. The description below can remain a single block — not everything needs to be split.

## Granularity Levels

1. **Single block** — the whole container enters at once (simplest, flattest)
2. **Sections** — title, description, buttons enter separately (~100ms stagger)
3. **Individual elements** — each word or item enters independently (~80ms stagger)

More granularity is not always better. Split the most important content (headlines) and keep supporting content as blocks. This maps to the selective emphasis pillar of [[design-taste]].

## With Motion

In Motion, use [[animate-presence]] with custom `transition.delay` per child instead of CSS custom properties:

```jsx
<motion.div
  initial={{ opacity: 0, y: 8, filter: "blur(5px)" }}
  animate={{ opacity: 1, y: 0, filter: "blur(0px)" }}
  transition={{ delay: index * 0.1 }}
/>
```

The stagger timing values in [[easing-reference]] (30-60ms per item) apply here — adjust based on how many items are entering and how much visual weight each carries.
