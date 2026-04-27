---
description: "Text polish techniques: balanced wrapping to prevent orphaned words and antialiased font smoothing for crisper rendering on macOS."
title: Text Rendering
---

# Text Rendering

Two CSS properties that quietly improve how text feels across an interface. Neither is dramatic on its own, but their absence is noticeable.

## Text Wrapping

`text-wrap: balance` distributes text evenly across lines, preventing orphaned words that dangle alone on the last line. Apply it to headings, cards, and any short text block where a single trailing word looks awkward.

```css
h1, h2, h3 {
  text-wrap: balance;
}
```

`text-wrap: pretty` is a lighter alternative — it only prevents orphans on the last line rather than rebalancing the entire block. Slightly better performance on long text, but `balance` produces cleaner results for short content.

**When to use which:**
- `balance` — headings, card titles, short descriptions (under ~6 lines)
- `pretty` — body text, longer paragraphs where full rebalancing would look odd

## Font Smoothing

On macOS, the default subpixel antialiasing renders text heavier than intended. Setting antialiased smoothing produces thinner, crisper letterforms — especially noticeable with light text on dark backgrounds.

```css
body {
  -webkit-font-smoothing: antialiased;
}
```

In Tailwind, apply `antialiased` to the body or layout wrapper:

```jsx
<body className="font-sans antialiased">
  {children}
</body>
```

Apply it globally — inconsistent smoothing across an interface is worse than either option alone. This connects to the simplicity pillar of [[design-taste]]: small inconsistencies compound into a feeling that something is off.

The visual difference is subtle but it affects the same perceptual layer as [[optical-alignment]] — trusting your eyes over default rendering.
