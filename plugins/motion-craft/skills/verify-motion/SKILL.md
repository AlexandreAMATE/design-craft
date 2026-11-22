---
name: verify-motion
description: Procedure to verify an implemented animation deterministically with a browser that can run JavaScript and take screenshots (for example Playwright MCP tools). Use after implementing or changing any CSS transition, CSS animation or Web Animations API motion, before declaring it done. Pauses and seeks animations, captures frames, checks durations, easings, properties, retargeting and reduced motion, and reports what could not be verified.
---

# Verify motion

A single screenshot cannot show motion. Pause the animations, seek them to fixed times and capture each frame. Project motion tokens and the project's art direction take precedence over any numeric default found in other skills.

**Limits.** This sees only CSS transitions, CSS animations and Web Animations API animations (`document.getAnimations()`). Canvas, WebGL and JS-driven libraries are invisible to it: they need a deterministic `renderAt(t)` hook exposed by the code. If none exists, say so in the report ("not verifiable") instead of guessing.

Tools needed: navigate, evaluate JavaScript in the page, screenshot, resize, emulate media. If one is missing, report it.

## Procedure

1. Open the real UI (dev server URL, not a mockup). Set the viewport. Put it in the "before" state and screenshot it.
2. Install the probe, then trigger the state change (click, focus, route change) and run the probe at once, in the same evaluate call when possible:
```js
const anims = document.getAnimations();
anims.forEach(a => a.pause());
window.__anims = anims;
return anims.map(a => {
  const t = a.effect.getComputedTiming(), k = a.effect.getKeyframes();
  return { target: a.effect.target?.tagName + '.' + a.effect.target?.className,
    kind: a.constructor.name, name: a.animationName || a.transitionProperty || a.id,
    props: [...new Set(k.flatMap(f => Object.keys(f)).filter(p => !['offset','easing','composite','computedOffset'].includes(p)))],
    duration: t.duration, delay: t.delay, endTime: t.endTime, easing: a.effect.getTiming().easing };
});
```
3. Seek and capture. For T = the longest `endTime`, repeat for 0, 25, 50, 75, 100 % (evaluate, then screenshot, five times):
```js
const T = Math.max(...window.__anims.map(a => a.effect.getComputedTiming().endTime));
window.__anims.forEach(a => { a.pause(); a.currentTime = T * PCT; }); // set PCT to 0, .25, .5, .75, 1
```
4. Finish: `window.__anims.forEach(a => a.finish())`, then screenshot the "after" state.
5. Retargeting: trigger the change again, let it run about halfway (`currentTime`), trigger the reverse, and screenshot right before and right after. The element must continue from its current position, not jump to the start or end. Run the probe again to read the new animations.
6. Layout shift: compare bounding boxes of the animated element and its siblings between the first and last frame:
```js
return [...document.querySelectorAll(SELECTOR)].map(e => { const r = e.getBoundingClientRect(); return [e.className, r.x, r.y, r.width, r.height]; });
```
7. Interaction: during the animation (paused mid-way is fine), check that the element or its container is not `pointer-events: none` or covered, unless that is intended.
8. Reduced motion: emulate `prefers-reduced-motion: reduce`, reload, repeat steps 1-4. Confirm no movement remains (no transform or size changes; opacity or instant changes only).

## Checks to report (table)

| Check | Result | Evidence |
|---|---|---|
| Durations and easings equal the project's motion tokens (name the token; flag every hard-coded value) | | probe output |
| Only `transform` and `opacity` animated (list any other property) | | `props` |
| Exit is shorter than enter | | durations |
| Nothing starts from `scale(0)` | | frame 0 keyframes |
| `transform-origin` matches the trigger (popovers, menus) | | computed style |
| No layout shift between first and last frame other than the intended one | | bounding boxes |
| Interaction not blocked during the animation | | step 7 |
| Retargets mid-flight without jumping | | step 5 frames |
| Reduced-motion pass clean | | step 8 frames |

## Output

Give: the frame screenshots (before, the five seek points, after), the table, and a plain statement of what could not be verified (JS-driven or canvas motion, missing tools, states not reachable). Never write "verified" for something you did not observe in a frame or probe result.
