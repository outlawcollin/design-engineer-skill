---
description: "Modern CSS pseudo-elements beyond ::before and ::after. View transitions, scroll markers, and native styling hooks that reduce JavaScript dependency for interactions."
title: Pseudo Elements
---

# Pseudo Elements

Most developers know `::before` and `::after`. They are workhorses for decorative elements, clearfixes, and icons. But CSS has shipped a new generation of pseudo-elements that provide direct styling hooks into browser-native features.

## ::before & ::after

These create anonymous inline elements as the first or last child of their parent. They require `content` to render. Common use cases: decorative layers, icons, separators, and expanding hit targets without adding DOM nodes.

A practical pattern: a button hover effect using `::before` with `position: absolute` and `inset: 0`. Set `transform: scale(0.95)` and `opacity: 0` by default. On hover, animate to `scale(1)` and `opacity: 1`. This creates a tactile feel without extra markup.

## View Transitions

The View Transitions API lets you animate between DOM states. Call `document.startViewTransition()`, the browser captures the current state, applies DOM changes, then generates pseudo-elements representing both states.

```css
::view-transition-group(card) {
  animation-duration: 300ms;
  animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
}
```

When two elements share the same `view-transition-name` across a transition, the browser morphs between their positions and sizes. This is a CSS-native alternative to [[shared-layout]] that does not require Motion or any JavaScript library.

The pattern: assign `view-transition-name` to the source element, inside the transition callback reassign it to the destination element. The browser interpolates automatically. Closing works in reverse.

## The Shift Away from JavaScript

`@starting-style` enables native CSS exit animations. Simple transitions no longer need JavaScript. But advanced patterns like reading presence state, manual exit control, and coordinated nested exits still require [[animate-presence]].

The direction is clear: browsers are absorbing capabilities that previously required libraries. Understanding these pseudo-elements helps you choose the lightest tool for each situation. Sometimes you don't need to install a library.
