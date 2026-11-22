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
