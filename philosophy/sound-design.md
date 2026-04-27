---
description: "Audio feedback on the web: why sound is the forgotten sense in web design, when it adds value, how to implement it without annoying users, and respecting user preferences."
title: Sound Design
---

# Sound Design

The web went mute by accident, not by design. Native apps use sound constantly for confirmations, errors, and notifications and nobody thinks less of them for it. The same goes for games. Yet on the web, sound is rare and frequently maligned.

The problem was never sound itself but how and when it was used: autoplaying music, loud error beeps, unnecessary clicks. Subtle, appropriate, optional sound is a different thing entirely.

## Why Sound Matters

The auditory cortex processes sound in about 25ms. Visual processing takes nearly ten times longer. A button that clicks feels faster than one that doesn't, even when the visual feedback is identical. Sound bridges the gap between action and response in a way visuals alone cannot.

A notification that chimes is present in your room, not just on your display. It crosses the boundary between device and environment. This connects to the secondary action principle in [[animation-principles]] — sound reinforces the primary visual feedback.

## The Emotional Layer

A single tone communicates success, error, tension, or playfulness. To achieve the same thing visually requires elaborate choreography. When sight and sound tell slightly different stories, we tend to believe our ears. A form submission with a gentle chime feels different than one met with silence. An error with a soft thunk lands differently than a red border alone.

This maps to the delight pillar of [[design-taste]] — sound is a delight multiplier that adds personality and presence.

## When to Use Sound

Not every interaction needs audio. Use sound where it adds value: confirmations for major actions like payments or uploads, errors and warnings that must not be overlooked, state changes that reinforce transitions, and notifications that interrupt without requiring visual attention. The sound should match the weight of the action.

## Respecting Preferences

There is no `prefers-reduced-audio` media query yet, but `prefers-reduced-motion` works as a reasonable proxy. Users who want less visual stimuli often want less audio stimuli too. Provide an explicit toggle in settings. Sound should always complement, never replace. Every audio cue must have a visual equivalent.

## Implementation

Basic audio playback is straightforward. Simple `Audio` objects cover most cases. The Web Audio API offers more power when needed. The implementation burden is low.

## Starting Small

Pick a single interaction that feels flat: a button that needs emphasis, a confirmation that gets overlooked, an action that would benefit from finality. Add a sound, make it subtle, make it optional. If it works, add another. Build the vocabulary gradually.
