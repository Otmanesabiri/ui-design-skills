# Exemple : Review d'un Formulaire

**Requête de l'utilisateur :** "Peux-tu faire une review de mon formulaire de paiement ? Il a l'air un peu brouillon."

## Review de l'Agent (Basée sur les UI Skills)

### Problèmes Bloquants 🔴
- **Boutons Concurrents :** Les boutons "Annuler" et "Payer" ont le même poids visuel (tous les deux avec un fond plein). **Correction :** Le bouton "Payer" doit être le bouton primaire (`var(--color-brand)`), et "Annuler" doit être secondaire (texte seul ou contour simple).
- **Loi de Fitts :** Les champs de texte et les boutons sont trop petits (hauteur de 32px). **Correction :** Augmenter la hauteur minimale à `44px` pour faciliter les clics, surtout sur mobile.

### Améliorations Majeures 🟡
- **Groupement Logique (Chunking) :** Les informations de la carte de crédit et l'adresse de facturation sont mélangées. **Correction :** Séparer en deux sections distinctes avec des titres clairs ("Informations de paiement" et "Adresse de facturation") avec un `margin-bottom` de `32px` (`var(--space-8)`) entre les sections.
- **Labels et Placeholders :** L'utilisation de placeholders au lieu de vrais labels au-dessus des champs nuit à l'accessibilité si l'utilisateur oublie ce qu'il remplissait. **Correction :** Placer des labels clairs au-dessus de chaque champ avec un espacement serré `var(--space-1)` (4px).

### Améliorations Mineures 🟢
- **Couleur des bordures :** Les bordures des champs utilisent un noir trop dur (`#000000`). **Correction :** Utiliser `var(--color-border-normal)` pour adoucir le rendu visuel.
- **Feedback visuel (Focus) :** L'état au clic sur un champ (focus) manque d'indication claire. **Correction :** Ajouter un contour de la couleur primaire (`var(--color-brand)`) lors du `focus` pour bien indiquer où l'utilisateur se trouve.

### Résultat Proposé
```css
/* Application des nouveaux tokens pour le formulaire */
.form-section {
  margin-bottom: var(--space-8); /* 32px */
}
.form-label {
  display: block;
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--color-text-primary);
  margin-bottom: var(--space-1); /* 4px */
}
.form-input {
  min-height: 44px; /* Accessible touch target */
  padding: var(--space-3);
  border: 1px solid var(--color-border-normal);
  border-radius: var(--radius-md);
  width: 100%;
}
.form-input:focus {
  outline: 2px solid var(--color-brand);
  border-color: transparent;
}
.btn-primary {
  background-color: var(--color-brand);
  color: var(--color-text-inverse);
  min-height: 44px;
  /* ... */
}
.btn-secondary {
  background-color: transparent;
  color: var(--color-text-secondary);
  /* ... */
}
```

### Résultat Attendu 👁️
Le formulaire sera transformé en une vue structurée : deux blocs distincts bien séparés (informations de carte, adresse). Les champs auront des labels lisibles au-dessus, et une hauteur généreuse de 44px rendant la saisie confortable. Les boutons d'action seront évidents : le bouton "Payer" ressortira massivement grâce à sa couleur de marque (`--color-brand`), tandis que le bouton "Annuler" sera discret. La saisie sera accompagnée d'un contour clair au focus, améliorant l'accessibilité globale.
