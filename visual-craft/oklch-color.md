---
description: "The OKLCH color model produces perceptually uniform palettes where changing only the hue keeps lightness consistent. Covers structure, gamut, gradients, Display-P3 support, maximum chroma, and CSS fallbacks."
title: OKLCH Color
---

# OKLCH Color

`oklch` is a color model designed to be perceptually uniform. Colors are accurate in terms of how humans perceive them, making palette creation and manipulation significantly easier than with `rgb` or `hsl`.

## Structure

OKLCH has three values: Lightness (0-1), Chroma (intensity, similar to saturation), and Hue (0-360 degrees). The underlying color space is OKLab.

```css
oklch(0.5 0.2 40)
/*    L    C   H  */
```

## Consistent Brightness

The major advantage: change only the hue and lightness stays consistent. Create four buttons with different colors by keeping L and C fixed, varying only H. In HSL, the same approach produces visually uneven results — some colors look lighter, others darker, some pop more.

## Predictable Shades

Change the lightness value to create shade scales without hue drift. OKLCH maintains consistent blueness across all shades. HSL drifts: lighter shades go purple, darker ones muddy toward gray.

## Gradients

OKLCH gradients interpolate through lightness, chroma, and hue rather than RGB values. This avoids muddy midpoints but can produce unexpected detour colors because hue is circular. For gradients, `oklab` interpolation is often more predictable because it moves in a straight line.

## Display-P3 Support

OKLCH can express colors outside the sRGB gamut that modern Display-P3 screens can show. If a display supports P3, OKLCH colors will appear more vivid. If not, the browser maps them back to sRGB.

## Maximum Chroma

OKLCH can define colors outside any real gamut. High chroma values get clipped to the nearest representable color, which can look very different from what was defined. Use maximum chroma calculations to stay within gamut boundaries.

## CSS Fallbacks

```css
@layer base {
  :root {
    --color-gray-100: #fcfcfc;

    @supports (color: oklch(0 0 0)) {
      --color-gray-100: oklch(0.991 0 0);
    }
  }
}
```

The browser uses OKLCH if supported, otherwise falls back to sRGB hex values.

This connects to [[design-taste]] through color intentionality — systematic, perceptually uniform palettes are a hallmark of crafted interfaces.
