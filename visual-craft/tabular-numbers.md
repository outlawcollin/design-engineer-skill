---
description: "Using tabular-nums to give digits equal width, preventing layout shift when numbers update in counters, timers, and prices."
title: Tabular Numbers
---

# Tabular Numbers

When numbers change — counters ticking up, prices updating, timers counting down — the surrounding layout should not shift. Proportional numerals have varying widths (a "1" is narrower than a "0"), causing visible jitter on every update.

`font-variant-numeric: tabular-nums` forces all digits to the same width:

```css
.counter {
  font-variant-numeric: tabular-nums;
}
```

In Tailwind: `tabular-nums`.

**Where to apply it:**
- Counters and timers
- Prices and currency displays
- Table columns with numeric data
- Progress indicators with percentage text
- Any number that updates dynamically

**Watch for font changes**: some typefaces (like Inter) subtly change the look of numerals when tabular spacing is applied. Check that the visual style still matches your intent.

This is a close relative of [[optical-alignment]] — both are about preventing visual jitter that breaks the sense of stability in an interface.
