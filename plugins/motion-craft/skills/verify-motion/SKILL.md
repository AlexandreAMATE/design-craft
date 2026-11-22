---
name: verify-motion
description: Verify a CSS or Web Animations API animation frame by frame in a real browser (pause, seek, screenshot, reduced-motion pass). Use after implementing or changing an animation, when browser automation tools are available.
---

# Verify motion

A single screenshot cannot show motion. Trigger the change, pause every animation in the same call, seek to fixed times and capture each frame. Project motion tokens and the project's art direction take precedence over any numeric default found in other skills.

Tools needed: browser automation tools (navigate, evaluate script, screenshot, resize, emulate media). If one is missing, say so in the report.

**Limits.**
- Only CSS transitions, CSS animations and Web Animations API animations are visible (`document.getAnimations()`). Canvas, WebGL and library-driven motion need a deterministic `renderAt(t)` hook exposed by the code; without one, report it as not verifiable.
- Infinite loops and scroll-driven animations are listed but not seeked (their end time is not finite). For loops, check off-screen pausing and the reduced-motion pass instead.
- `document.getAnimations()` does not enter shadow roots. Probe each one separately with `host.shadowRoot.getAnimations()`.

## Procedure

Snippets are function expressions: pass each one to the evaluate-script tool (with its argument). Never put a top-level `return` in a snippet.

1. Open the real UI (dev server URL, not a mockup), set the viewport, put it in the "before" state and screenshot it.
2. Probe. Trigger and pause in ONE call: a transition lasts 150-300 ms and would finish between two tool calls. The one-frame wait races `requestAnimationFrame` against a 50 ms timer because rAF may never fire in a hidden or headless page; seeking sets absolute times, so a late pause is harmless. `JSON.stringify` shows `Infinity` as `null`: a `null` `iterations` or `endTime` means an infinite loop. Adapt the trigger line (`root.click()`) when the state change is not a click (focus, hover state class, route change). `document.getAnimations()` is used rather than a subtree so portalled popovers are seen.
```js
async (sel) => { const root = document.querySelector(sel); root.click(); await Promise.race([new Promise(requestAnimationFrame), new Promise(r => setTimeout(r, 50))]);
  const anims = document.getAnimations().filter(a => a.timeline instanceof DocumentTimeline);
  anims.forEach(a => a.pause()); window.__anims = anims;
  return anims.map(a => { const e = a.effect, t = e.getComputedTiming(), el = e.target;
    return { target: el && el.localName + (el.id ? '#' + el.id : '') + (e.pseudoElement ?? ''), kind: a.constructor.name,
      name: a.animationName ?? a.transitionProperty ?? a.id, keyframes: e.getKeyframes(), effectEasing: e.getTiming().easing,
      transformOrigin: el ? getComputedStyle(el, e.pseudoElement ?? undefined).transformOrigin : null,
      delay: t.delay, duration: t.duration, iterations: t.iterations, endTime: t.endTime }; }); }
```
   Reading the result: the easing of a CSS animation is in `keyframes[i].easing` (`effectEasing` is `linear` for it); the easing of a transition is `effectEasing`. `keyframes` also gives the values (check for `scale(0)`), and `transformOrigin` the origin.
3. Seek and capture. Call with 0, 0.25, 0.5, 0.75, 1, taking a screenshot after each call:
```js
(pct) => { const f = window.__anims.filter(a => Number.isFinite(a.effect.getComputedTiming().endTime));
  const T = Math.max(...f.map(a => a.effect.getComputedTiming().endTime));
  f.forEach(a => { a.currentTime = Math.min(T * pct, a.effect.getComputedTiming().endTime - 0.001); });
  return `${f.length} seeked, ${window.__anims.length - f.length} infinite or scroll-driven skipped`; }
```
4. Release, then screenshot the "after" state:
```js
() => { window.__anims.forEach(a => { try { a.finish(); } catch { a.cancel(); } }); }
```
5. Retarget check (do not rely on live screenshots, they are not deterministic). Re-trigger from the "before" state, pause, seek to 50 %, read `getComputedStyle(el).transform`, trigger the reverse in the same call, wait one frame, then compare with the first transform keyframe of the new animation on `el`. Equal means it retargets from the current value; different means a jump.
```js
async (sel, elSel) => { const el = document.querySelector(elSel), root = document.querySelector(sel);
  root.click(); await Promise.race([new Promise(requestAnimationFrame), new Promise(r => setTimeout(r, 50))]);
  const a = el.getAnimations(); a.forEach(x => { x.pause(); x.currentTime = x.effect.getComputedTiming().endTime / 2; });
  const mid = getComputedStyle(el).transform; root.click(); await Promise.race([new Promise(requestAnimationFrame), new Promise(r => setTimeout(r, 50))]);
  const b = el.getAnimations().find(x => x.effect.getKeyframes()[0].transform), first = b && b.effect.getKeyframes()[0].transform;
  const tmp = document.createElement('div'); tmp.style.transform = first || 'none'; document.body.append(tmp);
  const norm = getComputedStyle(tmp).transform; tmp.remove(); // normalise to a matrix so the strings compare
  return { mid, first: norm, retargets: mid === norm }; }
```
   (Adapt: the reverse trigger may differ from the forward one. For CSS animations without a reverse, skip this step and say so.)
6. Layout shift: compare `getBoundingClientRect()` of the animated element and its siblings at seek 0 and seek 1.
7. Interaction: while paused mid-way, check that the element or its container is not unintentionally `pointer-events: none` or covered.
8. Reduced motion: emulate `prefers-reduced-motion: reduce`, reload and repeat steps 1-4. Decorative movement must be gone. Direct manipulation (drag tracking) and opacity or colour changes may remain.

## Checks to report (table)

| Check | Result | Evidence |
|---|---|---|
| Durations and easings equal the project's motion tokens (name the token, flag every hard-coded value) | | probe |
| Only `transform` and `opacity` animated (list any other property) | | `keyframes` |
| Exit shorter than enter | | durations |
| Nothing starts from `scale(0)` | | `keyframes` |
| `transform-origin` matches the trigger (popovers, menus) | | `transformOrigin` |
| No layout shift between first and last frame other than the intended one | | step 6 |
| Interaction not blocked during the animation | | step 7 |
| Retargets mid-flight without jumping | | step 5 |
| Reduced-motion pass clean | | step 8 |

## Output

Give the frame screenshots (before, the five seek points, after), the table, and a plain statement of what could not be verified (loops, scroll-driven, shadow roots, canvas or library motion, missing tools, unreachable states). Never write "verified" for something not seen in a frame or a probe result.
