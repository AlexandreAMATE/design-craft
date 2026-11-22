---
name: svg-scroll-recipes
description: Recipes for SVG stroke drawing and transform-origin fixes, scroll-driven animation with `@supports` fallbacks, clip-path reveals, and debugging an animation by symptom (slow, robotic, janky, jumping, flickering). Use when animating SVG, building scroll reveals or scrubbed scroll effects, doing clip-path reveals or sliders, or diagnosing why an animation feels wrong. Platform first (CSS, WAAPI, native scroll timelines).
---

# SVG, scroll and clip-path recipes

Platform-first recipes. Read only the reference that matches the task. Any library snippet inside them (Motion, flubber) is outside the platform and needs the project owner's approval (weight, licence, platform alternative). Numeric values are defaults: project motion tokens and art direction take precedence.

- `references/svg-animation.md` - SVG fundamentals, self-drawing strokes (`pathLength="1"` plus `stroke-dashoffset`), the `transform-origin` / `transform-box` trap, path morphing, shakes, ambient loops, busy-scene performance.
- `references/scroll-animations.md` - when a scroll animation should exist at all, triggered reveals vs scrubbed motion, CSS `animation-timeline` inside `@supports` with a readable fallback, parallax, sticky sections, never hijacking scroll.
- `references/clip-path-techniques.md` - `inset()` reveals, tab colour overlay, hold-to-delete, image reveal on scroll, comparison slider; compositing caveat for animated clip-path.
- `references/debugging-symptoms.md` - symptom to likely cause table: feels slow, robotic, cheap, janky, jumping, flickering.

For native CSS features (View Transitions, `@starting-style`, scroll-driven timelines) see the sibling `modern-web-guidance` and `css-native` skills.
