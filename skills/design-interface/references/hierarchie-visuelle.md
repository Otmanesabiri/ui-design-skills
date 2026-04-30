# 02 — Hiérarchie Visuelle

Sources : Refactoring UI ch.2 · Practical UI ch.4 (Layout) · Laws of UX ch.8 (Von Restorff)

---

## Principe fondamental

> "Quand tout dans une interface est en compétition pour l'attention, ça semble bruyant et chaotique — comme une lettre où chaque mot est souligné."

La hiérarchie visuelle est **le facteur le plus impactant** dans la perception d'un design comme "réussi". Elle précède tous les autres critères esthétiques.

**De-emphasiser les éléments secondaires est aussi important qu'emphasiser les primaires.**

---

## Les leviers de la hiérarchie

Ne pas utiliser uniquement la taille. Combiner plusieurs leviers :

| Levier | Usage | Exemple |
|--------|-------|---------|
| **Taille** | Différencier les niveaux majeurs | Titre H1 vs corps |
| **Poids (font-weight)** | Emphasiser sans changer la taille | `font-weight: 700` sur un label important |
| **Couleur / contraste** | Différencier primaire, secondaire, tertiaire | Noir pour le principal, gris moyen pour le secondaire, gris clair pour le tertiaire |
| **Espacement** | Grouper et séparer | Plus d'espace entre sections non liées |
| **Opacité** | Atténuer sans changer la couleur | `opacity: 0.5` sur du texte d'aide |

### Échelle de couleur pour la hiérarchie textuelle
```
Texte primaire    → hsl(220, 15%, 10%)   // quasi-noir
Texte secondaire  → hsl(220, 10%, 40%)   // gris moyen-foncé
Texte tertiaire   → hsl(220, 8%, 60%)    // gris moyen
Texte désactivé   → hsl(220, 5%, 75%)    // gris clair
```

---

## Hiérarchie des actions (boutons)

Chaque action sur une page occupe une position dans une pyramide d'importance.

### Les trois niveaux
```
Primaire   → Solid, couleur forte, visible immédiatement
Secondaire → Outline ou fond faible contraste, clair mais pas proéminent
Tertiaire  → Style lien, discret mais découvrable
```

### Règle critique
**La sémantique est secondaire à la hiérarchie.**

Un bouton "Supprimer" (danger) peut très bien être tertiary si ce n'est pas l'action principale de la page. Le style "danger = rouge" n'implique pas "danger = bouton primaire".

**Mauvais :**
```
[Sauvegarder]  [Supprimer]  ← deux boutons de même poids visuel
```

**Bon :**
```
[Sauvegarder]  Supprimer   ← supprimer est un lien, pas un bouton
```

### Maximum 1 bouton primaire par section
Si deux boutons semblent également importants, revoir la hiérarchie des actions — l'un des deux est forcément plus important.

---

## Hiérarchie des données (labels)

### Problème du format `Label: Valeur`
Ce format donne le même poids à chaque donnée. Il rend difficile de créer de la hiérarchie dans un ensemble de données.

### Alternatives par ordre de préférence

**1. Pas de label du tout**
Si le format de la donnée est auto-explicatif :
```
janedoe@example.com   ✓ (pas besoin de "Email :")
(555) 765-4321         ✓ (pas besoin de "Téléphone :")
$19.99                 ✓ (pas besoin de "Prix :")
```

**2. Label intégré dans la valeur**
```
12 en stock            ✓ (plutôt que "Stock: 12")
Membre depuis 2019     ✓ (plutôt que "Membre depuis: 2019")
```

**3. Label de support discret**
Si le label est nécessaire, le rendre secondaire visuellement :
```css
.label {
  font-size: 12px;
  font-weight: 500;
  color: hsl(220, 10%, 55%);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
.value {
  font-size: 16px;
  font-weight: 600;
  color: hsl(220, 15%, 10%);
}
```

**4. Label: Valeur** — uniquement en dernier recours

---

## The Squint Test (Practical UI)

Pour tester la hiérarchie d'une interface : **plisser les yeux jusqu'à ce que tout soit flou**.

Ce qui reste visible = éléments correctement priorisés.
Ce qui disparaît dans le bruit = éléments trop faibles.
Ce qui se détache trop = éléments trop forts.

Si tout disparaît au même rythme, la hiérarchie est absente.

---

## Von Restorff Effect (Laws of UX)

> "Parmi des objets similaires, celui qui diffère est le plus mémorisé."

### Application
- L'élément le plus important d'une page doit différer visuellement de ses voisins
- Un badge, une couleur d'accent, une taille différente — n'importe quelle rupture visuelle attire l'attention

### Mise en garde
**Ne pas sur-utiliser cet effet.** Si tout est mis en évidence, rien ne l'est. Réserver la différenciation pour 1 ou 2 éléments maximum par vue.

---

## Hiérarchie dans les formulaires multi-étapes

Structure recommandée :
```
Titre de l'étape     → H2, poids fort, couleur primaire
Sous-titre/contexte  → corps, couleur secondaire
Labels de champs     → uppercase small, couleur tertiaire
Valeurs des champs   → corps, couleur primaire
Actions              → bouton primaire seul à droite
Lien retour          → lien tertiary à gauche
```

---

## Profondeur comme levier de hiérarchie (Practical UI)

La profondeur (ombres, superposition) crée une hiérarchie spatiale :
- Éléments au premier plan (modales, dropdowns) → ombres fortes
- Éléments au niveau de la page (cartes) → ombres légères
- Éléments dans la page (fond de section) → pas d'ombre, différence de couleur de fond

```css
/* Niveaux d'élévation */
--shadow-sm: 0 1px 2px hsla(220, 15%, 10%, 0.08);         /* boutons */
--shadow-md: 0 4px 8px hsla(220, 15%, 10%, 0.12);         /* cartes */
--shadow-lg: 0 8px 24px hsla(220, 15%, 10%, 0.16);        /* dropdowns */
--shadow-xl: 0 16px 48px hsla(220, 15%, 10%, 0.20);       /* modales */
```