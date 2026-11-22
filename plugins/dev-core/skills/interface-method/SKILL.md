---
name: interface-method
description: Méthode du propriétaire pour toute tâche qui touche un composant, un style ou une animation d'interface web, y compris la 3D - interview frontend avec pistes visuelles à valider, implémentation, finition, vérification dans un navigateur, règles de mouvement. À charger par la session qui orchestre avant de planifier ou de déléguer un travail d'interface.
---

# Méthode d'interface

Les tokens et la direction artistique de la fiche projet priment sur toute valeur chiffrée d'un skill.
Paliers (définis dans les consignes globales) : gros = les quatre temps ; moyen = temps 2 et 4 ; trivial = test ciblé seulement.

## 1. Interview frontend (avant tout composant ou style nouveau)
Tu proposes d'abord ; tu ne me demandes pas de partir d'une page blanche.
1. **Audit** : relève les tokens, composants maison, animations et la direction artistique existants (`dev-core:design-system`, qui en dresse l'inventaire) pour ne proposer que ce qui s'y raccorde.
2. **Proposition** avec `frontend-design:frontend-design` : l'intention en une phrase, puis deux ou trois pistes réellement différentes, dont une plus audacieuse. Pour chacune : composition, typographie, couleurs, densité, mouvement (quoi bouge, quand, pourquoi, en chiffres) et tous les états (vide, chargement, erreur, survol, focus, désactivé). Dis laquelle tu recommandes et ce qui la distingue d'une interface générique.
3. **Montrer plutôt que décrire** : dès que le choix est visuel, une maquette HTML autonome construite avec les tokens du projet (`playground:playground`, gabarit `design-playground`). Donne-moi le chemin du fichier à ouvrir.
4. **Questions** : seulement ce que la proposition ne peut pas trancher sans moi (ton, références aimées ou rejetées, niveau d'audace, priorités), en boîte de dialogue.
5. **Trace** : ce que je valide entre dans la spec du chantier ; ce qui vaut pour tout le projet entre dans la direction artistique de la fiche projet. Si le projet n'a pas de direction artistique écrite, cette interview sert d'abord à la constituer.

## 2. Implémentation
Agent généraliste (sonnet) ; nomme dans son brief les skills utiles, par leur nom exact :
- React et styles : `dev-core:react-patterns`, `dev-core:frontend-patterns`, `dev-core:react-testing` ; composants et tokens du projet d'abord.
- Animation d'interface : `motion-craft:animate`, puis au besoin `motion-craft:choreograph`, `motion-craft:gestures`, `motion-craft:animation-performance`, `motion-craft:emil-design-eng`.
- Sans bibliothèque : `web-platform-motion:modern-web-guidance` (View Transitions, animations liées au défilement, `@starting-style`, `linear()`), `web-platform-motion:css-native` (syntaxe), `web-platform-motion:svg-scroll-recipes` (tracé SVG, défilement, `clip-path`), `web-platform-motion:canvas-generative`.
- 3D : `threejs-skills:threejs-fundamentals` puis les autres skills `threejs-skills:threejs-*` selon le sujet ; conception de la scène sur opus. Chargement différé, modèles compressés, plafond de résolution, repli statique si WebGL manque ou en mouvement réduit, libération des ressources au démontage ; aucun fichier téléchargé à l'exécution.

Choisis l'outil le plus léger qui suffit : CSS et tokens ; puis Web Animations API, View Transitions, animations liées au défilement, Canvas ; Three.js pour la 3D. Toute bibliothèque d'animation ou de 3D absente de la fiche projet se propose en interview (poids, licence, alternative sans elle) et n'entre qu'avec mon accord.

## 3. Finition (distincte de la revue de code)
`ui-polish:better-interface` sur ce qui vient d'être construit (rayons, ombres, espacements, typographie, zones cliquables, états d'interaction).

## 4. Vérification et revue
- Un agent généraliste avec les outils de navigateur ouvre l'interface réelle et joue le parcours ; captures avant et après dans le rapport. `dev-core:click-path-audit` relit le code des gestionnaires si un parcours casse.
- Toute animation : `motion-craft:review-animations` puis `motion-craft:verify-motion` (pause, avance image par image, passe en mouvement réduit). Jamais de jugement sur une capture unique.
- Revue : `ui-polish:interface-review` sur le diff ; `dev-core:react-reviewer` sur le `.tsx` ; accessibilité par les tests du projet et un agent généraliste chargé de `dev-core:frontend-a11y` (clavier, contraste, lecteur d'écran, mouvement réduit).
- Si l'interface ne s'ouvre pas dans un navigateur (webview d'extension, application embarquée), dis-le dans le rapport et propose le banc d'essai manquant ; ne saute pas l'étape en silence.

## Règles de mouvement
- Toute durée, courbe ou ressort passe par les tokens du projet ; aucune valeur en dur ; une seule famille de courbes dans l'app. Le mouvement s'écrit en chiffres (durée, courbe, états), jamais en adjectifs.
- Interactions sous 300 ms ; les durées longues sont réservées aux moments rares.
- Par défaut `transform` et `opacity`. `clip-path` et `stroke-dashoffset` sont admis pour les moments rares, après mesure. Les View Transitions servent aux changements de vue ou d'état d'ensemble, pas aux micro-interactions.
- Rien sur ce qu'on fait cent fois par jour (menus, raccourcis clavier, frappe). Une animation ne bloque jamais une action et s'interrompt proprement.
- La sortie est plus courte que l'entrée ; rien ne part d'une échelle 0 ; un popover grandit depuis son déclencheur.
- Mouvement réduit : plus de déplacement décoratif ; fondus et changements instantanés restent.
- La patte vient de la cohérence, plus un ou deux moments signature rares et soignés, proposés en interview. Pas d'effet décoratif en boucle.
