# Contexte et Vocabulaire (Shared Language)

Ce document définit le vocabulaire et les conventions partagées pour l'ensemble du projet de design UI.

## 1. Principes Fondamentaux
- **Design Tokens** : Les plus petites briques de design (couleurs HSL, tailles en rem, espacements en multiples de 4px). Aucun style "en dur" (hardcoded) ne doit être utilisé.
- **Accessibilité by Design** : Le contraste (WCAG AA), les tailles des zones de clic (min 44x44px) et la lisibilité ne sont pas des options de fin de projet.
- **Itération Monochrome** : Toujours commencer par définir l'interface en niveaux de gris (grayscale) pour valider la hiérarchie et les contrastes avant d'introduire de la couleur.

## 2. Vocabulaire Standardisé
- **Surface** : L'arrière-plan d'un conteneur ou d'une page (`--surface-1`, `--surface-2`).
- **Accent** : La couleur principale utilisée pour attirer l'attention (boutons primaires, liens, états actifs).
- **Muted** : Couleurs adoucies pour les éléments secondaires ou tertiaires (textes secondaires, bordures subtiles).
- **Chunking** : Regroupement visuel d'informations reliées pour réduire la charge cognitive (Loi de Miller).
- **HSL Mirroring** : Technique de création de mode sombre consistant à conserver la teinte (Hue) et la saturation (Saturation) mais à inverser la luminosité (Lightness).

## 3. Conventions de Code et CSS
- Utiliser le système `rem` pour la typographie (où 1rem = 16px par défaut).
- Utiliser des variables CSS (`var(--nom-du-token)`) pour chaque valeur de design.
- Les espacements suivent une échelle stricte basée sur 4px (ex: `var(--space-1)` = 4px, `var(--space-2)` = 8px).

Ce contexte garantit une communication claire et des choix de design cohérents tout au long de la création ou de l'amélioration des interfaces.
