# Provenance - web-platform-motion

Four skills from three upstream repositories.

## modern-web-guidance (Apache-2.0)
- Source: https://github.com/GoogleChrome/modern-web-guidance
- Commit: b31dc0a43ff5d19bcf386a3476a216f3b39a6f55 (2026-10-12T20:16:22+00:00)
- Licence: Apache-2.0 (`LICENSE`). The upstream has no NOTICE file.
- Kept: guides under `skills/modern-web-guidance/guides/` in the categories ui-behaviors (all), css (all), visual-design (all), ui-atoms (all, scroll-driven UI patterns), performance/faster-spa-view-transitions.md, forms/animated-select-picker.md, ui-components/{spinner,progress-ring,navigation-drawer,stack-drill-down,hovercard,checkbox}.md (all other guides in those folders mention animation, view transitions or scroll timelines).
- Dropped: skills/chrome-extensions, the upstream skills/modern-web-guidance/SKILL.md, guide categories accessibility, built-in-ai, html, js, privacy, pwa, security, wasm, webmcp, the rest of forms, performance and ui-components; root files (README, package.json, manifests for other agents, policies, assets, .github).
- Modifications (Apache-2.0 section 4(b): changed files carry prominent notice here):
  - `skills/modern-web-guidance/SKILL.md`: NEW file written for this marketplace (frontmatter, usage instructions, generated index). Replaces the upstream one, which is not copied.
  - 54 occurrences in the guides of the form "(via `npx -y modern-web-guidance@latest retrieve \"<name>\"`)" were replaced by "(guide `<path>`)" or "(guide not included in this trimmed snapshot)". Files touched: those among the kept guides that contained such a reference (css/*, ui-behaviors/*, visual-design/*, ui-atoms/*, ui-components/*). Why: no network/npx instruction, and the tool is not available.
  - `skills/modern-web-guidance/guides/ui-behaviors/physics-based-easing.md`: the "JavaScript Library Fallback (Motion/GSAP)" recommendation was replaced by the neutral note "outside the platform: propose a permissively licensed library to the project owner (weight, licence, platform alternative) before using it"; the Motion code example is kept as illustration. Why: library recommendation policy.
  - No other content change. Guides still contain illustrative polyfill CDN URLs and `npm install` snippets; SKILL.md states that these need project owner approval.

## css-native and canvas-generative (MIT)
- Source: https://github.com/AThevon/genjutsu (path skills/_jutsu/<skill>)
- Commit: a22540b623590505879d6489dd03d7f3072bce05 (2026-11-16T02:50:12+01:00)
- Licence: MIT (`LICENSE-genjutsu-MIT`)
- Kept: css-native/SKILL.md, css-native/references/modern-css.md, canvas-generative/SKILL.md, canvas-generative/references/algorithms.md.
- Dropped: every other genjutsu skill (cast, paint, bunshin, orchestration, gsap, framer-motion, etc.), _jutsu/VERSIONS.md, scripts, evals, packaging, docs.
- Modifications:
  - Both SKILL.md: removed `metadata.internal: true`; removed the pointer to `_jutsu/VERSIONS.md` in the version-sensitive banner.
  - `css-native/SKILL.md`: in the "CSS Native vs Library" table the recommendations GSAP, Framer Motion and GSAP MorphSVG were replaced by "Outside the platform: propose a permissively licensed library to the project owner (weight, licence, platform alternative) before using it" (with the factual native-limits remarks kept); the closing rule of thumb now says to propose a library to the owner first.
  - `canvas-generative/SKILL.md`: the "Loading Sub-skills" table pointing to `../motion-principles` and `../threejs-r3f` now says "not covered here" and names the sibling marketplace plugins; heading renamed "Quick Reference".
  - No shell `cat` loading blocks or references to cast/paint/bunshin existed in these two skills (checked by grep).

## svg-scroll-recipes (MIT)
- Source: https://github.com/mblode/agent-skills (path skills/ui-animation/references/)
- Commit: ff9805a3dabf4529f4d88f6b3f09c5a33cb0fcb6 (2026-11-20T09:40:48+11:00, verified on disk)
- Licence: MIT, "Copyright (c) 2026 Matthew Blode" (`LICENSE-mblode-MIT`, copied from upstream LICENSE.md)
- Kept: references/svg-animation.md, scroll-animations.md, clip-path-techniques.md, debugging-symptoms.md (names matched exactly).
- Dropped: upstream ui-animation SKILL.md, all other references, scripts/ (python), evals/, and every other skill of the repo.
- New (original, MIT): `skills/svg-scroll-recipes/SKILL.md`, a thin index written for this marketplace.
- Modifications:
  - `svg-animation.md`: the stroke-draw recipe now sets `pathLength="1"` on the path (explicit step, HTML snippet, CSS comment) so `stroke-dasharray: 1px 1.1px` is correct; the `pathLength="100"` bullet was reworded to match. Why: without it the dash does not equal the path length.
  - `svg-animation.md`: standard note "Outside the platform: needs the project owner's approval (weight, licence, platform alternative)" inserted before 4 Motion code blocks and after the flubber sentence; pointer to `performance-deep-dive.md` replaced by "(with an IntersectionObserver)".
  - `clip-path-techniques.md`: "hardware-accelerated" claims (intro and comparison slider) replaced by: compositing of clip-path animations is not reliable across browsers, measure before relying on it, prefer transform/opacity when possible.
  - `scroll-animations.md`: same standard note after the Motion `useScroll` item; "still not Baseline" reworded to "was not Baseline when written (re-check current support)".
  - `debugging-symptoms.md`: removed pointers to `performance-deep-dive.md` (two places) and `component-patterns.md` (replaced by `interpolate-size` / `calc-size()` hint).

## Review-fix changes (round 3)
- Original files (Copyright (c) 2026 design-craft maintainers, MIT): `skills/modern-web-guidance/SKILL.md`, `skills/svg-scroll-recipes/SKILL.md`. See `NOTICE-design-craft.md`.
- `modern-web-guidance/SKILL.md`: description rewritten; note extended to `import("https://...")` and `@latest` CDN imports (never add a runtime CDN import; vendor a pinned copy with owner approval); `css-layout.md` index topic corrected.
- Modified Chrome guides (19) now start with `<!-- Modified by design-craft: see PROVENANCE.md -->`: `css/css-layout.md`, `css/css.md`, `css/responsive-design.md`, `css/usage-aware-component-variations.md`, `ui-atoms/component-specific-light-dark-theme.md`, `ui-behaviors/drag.md`, `ui-behaviors/motion.md`, `ui-behaviors/physics-based-easing.md`, `ui-behaviors/spatial-navigation.md`, `ui-behaviors/swipe-to-remove.md`, `ui-behaviors/swipe-to-reveal.md`, `ui-components/hovercard.md`, `ui-components/progress-ring.md`, `ui-components/spinner.md`, `visual-design/browser-ui-theming.md`, `visual-design/color.md`, `visual-design/dark-mode.md`, `visual-design/equal-width-text-lines.md`, `visual-design/visual-effects.md`. Their edits are the `npx retrieve` reference replacements, plus `ui-behaviors/physics-based-easing.md`: the library-fallback heading and paragraph, and the code comment "Example using Motion (motion.dev) for a spring fallback." (reworded to "Example using a spring library (Motion) for a fallback, shown only as a technical illustration.").
- `css-native/SKILL.md`: previously undeclared edit declared: heading "When to Use CSS Native vs Library" renamed "vs a Library". Description rewritten (syntax cheat sheet). Precedence line added to `css-native` and `canvas-generative`. In `css-native` (SKILL.md and references/modern-css.md): `ease`, `ease-in`, `ease-out` in code blocks replaced by `var(--ease-out)` (and the Material `cubic-bezier(0.4, 0, 0.2, 1)` by the same token); durations above 300 ms annotated "page-level or scroll-linked only, not component interactions"; "composite-only ... GPU" line and the performance table row for `filter` / `clip-path` corrected (clip-path compositing not reliable across browsers, measure); scroll-driven-animations.style tool pointer removed.
