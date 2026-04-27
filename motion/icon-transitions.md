---
description: "Animating opacity, scale, and blur when icons swap contextually using AnimatePresence with popLayout mode. Makes any icon state change feel intentional rather than instant."
title: Icon Transitions
---

# Icon Transitions

When icons change based on state (copy → check, play → pause), animating the swap with opacity, scale, and blur makes the transition feel intentional.

## The Progression

**No animation**: icon swaps instantly. Functional but lifeless.

**Opacity only**: crossfade between icons. Better, but flat.

**Opacity + scale + blur**: the outgoing icon shrinks, blurs, and fades while the incoming one grows, sharpens, and appears. This is the quality target.

## Implementation

Wrap the conditional icon in [[animate-presence]] with `popLayout` mode:

```jsx
<button onClick={handleCopy}>
  <AnimatePresence mode="popLayout" initial={false}>
    <motion.div
      key={isCopied ? "check" : "copy"}
      initial={{ opacity: 0, scale: 0.25, filter: "blur(4px)" }}
      animate={{ opacity: 1, scale: 1, filter: "blur(0px)" }}
      exit={{ opacity: 0, scale: 0.25, filter: "blur(4px)" }}
      transition={{ type: "spring", duration: 0.3, bounce: 0 }}
    >
      {isCopied ? <CheckIcon /> : <CopyIcon />}
    </motion.div>
  </AnimatePresence>
</button>
```

The `key` prop is critical — it tells `AnimatePresence` when to trigger the exit/enter cycle. `initial={false}` prevents the animation on first render.

`popLayout` mode removes the exiting icon from document flow immediately, preventing layout shift during the transition.

## CSS Alternative

The same effect is achievable with CSS transitions on opacity, scale, and filter. Motion is preferred for spring animations which create more natural-feeling transitions, but CSS works for simple cases.

This technique connects to the squash and stretch principle in [[animation-principles]] — the scale change gives icons a sense of physicality. For more complex icon animation (shape morphing rather than swapping), see [[icon-morphing]].
