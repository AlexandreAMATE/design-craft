# design-craft

Marketplace Claude Code local, composé de copies filtrées et vérifiées de packs de skills open source (UI motion, CSS natif, three.js). Uniquement du markdown et du texte : aucun script, hook, MCP, agent ni commande.

## Plugins

| Plugin | Skills |
|---|---|
| `motion-craft` | animate, emil-design-eng, review-animations, choreograph, animation-performance, gestures, animation-vocabulary, verify-motion (original : procédure de vérification d'animation avec un navigateur piloté) |
| `ui-polish` | better-ui, better-layout, better-typography, better-interface, interface-review (manuel uniquement : `disable-model-invocation: true`) |
| `web-platform-motion` | modern-web-guidance (93 guides + index), css-native, canvas-generative, svg-scroll-recipes (références SVG, scroll, clip-path, débogage par symptôme) |
| `threejs-skills` | threejs-animation, -asset-pipeline, -fundamentals, -geometry, -interaction, -lighting, -loaders, -materials, -performance, -postprocessing, -react-three-fiber, -shaders, -textures |

## Provenance

| Plugin | Source | Commit | Date | Licence |
|---|---|---|---|---|
| motion-craft | github.com/emilkowalski/skills | 64eb3deb9a5fbfa041faf783e0bc3fd635872e9c | 2026-11-15 | MIT |
| web-platform-motion (guides) | github.com/GoogleChrome/modern-web-guidance | b31dc0a43ff5d19bcf386a3476a216f3b39a6f55 | 2026-10-12 | Apache-2.0 |
| web-platform-motion (css-native, canvas-generative) | github.com/AThevon/genjutsu | a22540b623590505879d6489dd03d7f3072bce05 | 2026-11-16 | MIT |
| web-platform-motion (svg-scroll-recipes) | github.com/mblode/agent-skills | ff9805a3dabf4529f4d88f6b3f09c5a33cb0fcb6 | 2026-11-20 | MIT |
| ui-polish | github.com/jakubkrehel/skills | 672ae44ace6aaed65b86cbb1e2fd6fbea0e79578 | 2026-11-18 | MIT |
| motion-craft / verify-motion | original | - | - | MIT |
| threejs-skills | github.com/CloudAI-X/threejs-skills | 0e181866f095b5f06d005133876e926515390d95 | 2026-10-19 | MIT |

Détail des fichiers gardés, écartés et des modifications : `plugins/<nom>/PROVENANCE.md`.

## Règle de priorité

Les tokens et la direction artistique du projet priment sur toute valeur chiffrée (durées, easings, échelles, espacements) d'un skill de ce marketplace. Les valeurs des skills ne sont que des défauts.

## Ajout aux réglages gérés de Claude Code

Héberger ce dépôt sur un serveur git interne (l'hôte ci-dessous est un exemple), puis, dans `managed-settings.json` :

```json
{
  "strictKnownMarketplaces": [
    { "source": "github", "repo": "your-org/design-craft", "ref": "<tag-ou-sha-valide>" }
  ],
  "extraKnownMarketplaces": {
    "design-craft": {
      "source": { "source": "github", "repo": "your-org/design-craft", "ref": "<tag-ou-sha-valide>" }
    }
  },
  "enabledPlugins": {
    "motion-craft@design-craft": true,
    "web-platform-motion@design-craft": true,
    "threejs-skills@design-craft": true,
    "ui-polish@design-craft": true
  }
}
```

Pour un hôte autre que GitHub, utiliser `{ "source": "git", "url": "...", "ref": "..." }`. L'entrée de la liste blanche doit correspondre exactement (url, ref, path) à la source déclarée.

## Mise à jour

1. Re-cloner chaque amont (shallow) à un nouveau SHA dans un dossier vide, sans exécuter quoi que ce soit.
2. Recopier uniquement les fichiers listés dans le `PROVENANCE.md` du plugin, puis ré-appliquer les modifications qui y sont décrites.
3. Régénérer l'index de `modern-web-guidance/SKILL.md` et mettre à jour SHA et dates (PROVENANCE, README, SKILL.md).
4. Relancer les contrôles (JSON valide, frontmatter, extensions autorisées, grep des motifs sensibles, liens relatifs, tailles) puis `claude plugin validate .`.
5. Committer, puis publier un nouveau tag/SHA et mettre à jour `ref` dans les réglages gérés.
