---
description: "The 12 principles of animation adapted for UI: squash and stretch, anticipation, staging, straight ahead vs pose to pose, follow-through, slow in/out, arcs, secondary action, timing, exaggeration, solid drawing, and appeal."
title: Animation Principles
---

# Animation Principles

The 12 Principles of Animation were developed by Disney animators in the 1930s. They are observations about how humans perceive movement, and they translate directly to interface design. Every technique in [[motion]] traces back to at least one of these principles.

## Squash and Stretch

Everything has mass, and the way it deforms conveys weight and personality. Use this to create elements that feel malleable and responsive. In UI, a wallet icon that squashes on selection or a button that compresses on tap communicates physicality. Use in moderation — overdoing it creates a cartoonish effect.

## Anticipation

Prepare users for what comes next. A notification icon that wiggles implies updates awaiting. A hold-to-delete interaction gives the user time to reconsider. This is about giving cues before major actions, not adding delay to every interaction. Save it for moments where an extra hint helps.

## Staging

If anticipation is about the before, staging is about the during. Focus user attention on what matters most as an interaction unfolds. A backdrop blurs first, then the panel slides in, then the primary control highlights. Choreograph the sequence. Avoid animating too many things simultaneously — [[animate-presence]] with `popLayout` mode helps coordinate this.

## Straight Ahead Action & Pose to Pose

On the web, we define keyframes and let the browser interpolate. Consider how often an action will be used: Apple only animates context menus on exit because animating both in and out on a frequent action feels sluggish. The frequency-to-animation mapping connects directly to the Delight-Impact Curve in [[design-taste]].

## Follow-Through & Overlapping Action

Not everything starts or stops at the same time. A list where each card enters with a tiny stagger relative to the previous card turns a static block into a dynamic flow. Springs make this feel more alive — stiffness, damping, and mass create natural follow-through. Use it to soften any transition that feels jarring. The [[collection-preview]] pattern demonstrates this with spring-driven hover effects.

## Slow In & Slow Out

Most things in nature don't start or stop instantly. This principle is the cornerstone of easing curves. An `ease-out` makes elements feel snappy. An `ease-in` works for elements entering the viewport. The golden curve `cubic-bezier(0.16, 1, 0.3, 1)` captures this perfectly. See [[easing-reference]] for the full table and [[will-change-performance]] for why easing on compositor-friendly properties is cheap.

## Arcs

Arcs make movement feel organic. Instead of sliding elements in straight lines, a gentle curve adds realism. Hard to implement well in UX — more relevant for landing pages and hero sections than functional UI. Experimentation is needed.

## Secondary Action

Little flourishes that support the main action without stealing the spotlight. A checkmark that pops and then sparkles after form submission. [[sound-design]] is itself a secondary action: a subtle click reinforcing the visual feedback of a button press.

## Timing

The speed of an action. A tooltip at 150ms feels right; at 400ms it feels annoying. Keep durations under 300ms for most interactions. Define timing guidelines and reuse them — see [[easing-reference]]. Consistent timing across similar actions keeps the experience coherent.

## Exaggeration

Intentionally amplifying a motion to make a point. An error wiggle on a form field is exaggeration: the field shakes to draw attention. Use sparingly for moments when you want the user to feel something strongly. At home in onboarding, empty states, confirmations, and error notifications.

## Solid Drawing

Making objects feel three-dimensional in their space. Use shadows, layering, and perspective to communicate hierarchy. The CSS `perspective` property creates depth for 3D transforms. Consistency matters: if an icon rotates in 3D, it shouldn't suddenly look flat. This connects to [[shadows-over-borders]] for creating depth and [[concentric-border-radius]] for maintaining visual consistency.

## Appeal

Everything tied together into an experience that is visually and emotionally compelling. The difference between technically usable and something people want to use. Think of the products you find delightful — what makes them special is attention to detail, playful interactions, and anticipation of user needs. This maps directly to the delight pillar of [[design-taste]].
