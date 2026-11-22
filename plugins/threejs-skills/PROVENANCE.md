# Provenance - threejs-skills

- Source: https://github.com/CloudAI-X/threejs-skills
- Commit: 0e181866f095b5f06d005133876e926515390d95 (2026-10-19T08:17:17+03:00)
- Licence: MIT (see `LICENSE`)

## Files kept
- `skills/threejs-animation/SKILL.md`
- `skills/threejs-asset-pipeline/SKILL.md`
- `skills/threejs-fundamentals/SKILL.md`
- `skills/threejs-geometry/SKILL.md`
- `skills/threejs-interaction/SKILL.md`
- `skills/threejs-lighting/SKILL.md`
- `skills/threejs-loaders/SKILL.md`
- `skills/threejs-materials/SKILL.md`
- `skills/threejs-performance/SKILL.md`
- `skills/threejs-postprocessing/SKILL.md`
- `skills/threejs-react-three-fiber/SKILL.md`
- `skills/threejs-shaders/SKILL.md`
- `skills/threejs-textures/SKILL.md`
- `LICENSE`

## Files dropped
README.md (upstream root readme), .git.

## Modifications
- `skills/threejs-asset-pipeline/SKILL.md`: before each of 7 code blocks that run `npx` (gltf-transform CLI, gltfjsx) a one-line note was inserted: "this step downloads a tool with npx and needs the project owner's approval before it is run". Commands themselves unchanged. The inline wrong-to-right bullet list near the end also contains npx commands and was left unchanged (covered by the notes above).

## Review-fix changes (round 3)
- API names target three r186; confirm against the installed three version's docs before use. The reviewer could not confirm `Object3D.pivot`, `SunLight`, `setEffects`, `retroreflectivity` and `RenderPipeline` against the three.js docs. A one-line note with this text was added at the top of `threejs-geometry`, `threejs-lighting`, `threejs-materials` and `threejs-postprocessing` SKILL.md. Technical content untouched.
- `threejs-fundamentals/SKILL.md`: approval note before both jsDelivr importmap blocks (runtime CDN load). `threejs-asset-pipeline/SKILL.md`: approval note before the "install KTX-Software first" paragraph and before the remaining `npx` bullet list. `threejs-react-three-fiber/SKILL.md`: note that `<Environment preset=...>` and the default Draco decoder path download assets at runtime; ship local HDRI and decoder files instead.
- No original files (`NOTICE-design-craft.md` added for uniformity).
