# 05 — Espacement, Layout & Profondeur

Sources : Refactoring UI ch.3 (Spacing & Layout) · Practical UI ch.4 (Layout and Spacing)

---

## Système d'espacement

### Règle fondamentale
Définir un ensemble de valeurs prédéfinies. Ne jamais inventer une valeur arbitraire.

### Échelle recommandée (base 4px)
```
4px   → micro (séparation d'icône et label, gap interne)
8px   → xs (padding interne compact)
12px  → sm (padding bouton small, gap entre éléments proches)
16px  → md (padding standard, gap entre champs de formulaire)
24px  → lg (padding card, séparation de sections liées)
32px  → xl (séparation de blocs)
48px  → 2xl (séparation de sections)
64px  → 3xl (séparation de sections majeures)
96px  → 4xl (marges de page sur desktop)
128px → 5xl (espacement hero)
```

### En CSS (custom properties)
```css
:root {
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-6: 24px;
  --space-8: 32px;
  --space-12: 48px;
  --space-16: 64px;
  --space-24: 96px;
  --space-32: 128px;
}
```

En Tailwind, ce système correspond à `p-1, p-2, p-3, p-4, p-6, p-8, p-12, p-16, p-24, p-32`.

---

## Espacer selon la proximité logique

### Principe de Gestalt : proximité
Les éléments proches sont perçus comme liés. L'espacement est le premier outil de groupement.

**Règle :** L'espace entre deux éléments non liés doit être **significativement plus grand** qu'entre deux éléments liés.

```
Titre de section
  Paragraphe lié au titre    ← petit espacement entre titre et contenu
  
                             ← grand espacement avant la section suivante
Section suivante
```

### L'espacement ambigu est une erreur
Si l'espace entre A et B est identique à l'espace entre B et C, l'utilisateur ne sait pas si B est lié à A ou à C. Choisir explicitement.

---

## White space : être généreux

La majorité des interfaces manquent d'espace, pas le contraire.

### Erreurs fréquentes
- Boutons avec padding insuffisant (`padding: 4px 8px` pour un bouton primaire)
- Cartes avec contenu trop serré contre les bords
- Sections avec trop peu d'espace entre elles
- Texte dans un input trop proche du bord

### Règle pratique
Si l'interface semble "chargée", essayer de doubler l'espacement partout. La plupart du temps, ça améliore immédiatement.

---

## L'espacement ne se scale pas proportionnellement

### Le problème du scaling relatif
Si un bouton `sm` a `padding: 4px 8px` et un bouton `lg` a `padding: 12px 24px`, le bouton `lg` ne fait pas simplement "3x le padding sm" — il a un padding **proportionnellement plus généreux**.

Les grands éléments ont un padding **relativement plus grand** que les petits, pas juste plus grand en valeur absolue.

```css
/* MAUVAIS : scaling proportionnel uniforme */
.btn-sm { padding: 4px 8px; font-size: 12px; }   /* ratio 1:2 */
.btn-md { padding: 8px 16px; font-size: 16px; }  /* ratio 1:2 */
.btn-lg { padding: 12px 24px; font-size: 20px; } /* ratio 1:2 */

/* BON : padding relativement plus généreux sur le grand */
.btn-sm { padding: 4px 10px; font-size: 12px; }
.btn-md { padding: 10px 20px; font-size: 16px; }
.btn-lg { padding: 16px 32px; font-size: 20px; } /* plus généreux en proportion */
```

---

## Grilles

### Grille 12 colonnes comme base
Aligner le layout principal sur une grille 12 colonnes. Elle offre suffisamment de flexibilité (divise par 1, 2, 3, 4, 6, 12).

### Les grilles ne sont pas des règles absolues
Pas tous les éléments doivent être fluides et basés sur des pourcentages :
- Une sidebar peut avoir une largeur fixe (240px, 280px)
- Une modal a une largeur max fixe
- Un input a une largeur idéale selon le contenu attendu

**Ne pas outsourcer toutes les décisions de layout à la grille.**

---

## Groupement (Gestalt)

### Common Region : les conteneurs créent les groupes
Les éléments à l'intérieur d'un même conteneur (bordure, fond, ombre) sont perçus comme appartenant au même groupe.

```
┌─────────────────────┐
│ Élément A           │  ← A et B sont perçus comme liés
│ Élément B           │
└─────────────────────┘

  Élément C              ← C est perçu comme séparé
```

### Types de conteneurs (du plus fort au plus subtil)
1. **Background color** différent → groupe fort
2. **Bordure** → groupe fort
3. **Ombre (box-shadow)** → groupe fort
4. **Proximité seule** → groupe implicite, moins puissant

---

## Ombres et profondeur

### Principe de la source de lumière
La lumière vient **du haut**. Simuler cela en interface :

- **Éléments surélevés** → bord supérieur plus clair + ombre sous l'élément
- **Éléments en creux** (inset) → ombre en haut + bord inférieur plus clair

### Système d'élévation (5 niveaux)

```css
:root {
  /* Niveau 0 : au niveau de la surface, pas d'ombre */
  --shadow-none: none;

  /* Niveau 1 : légèrement surélevé — boutons, badges */
  --shadow-sm:
    0 1px 2px hsla(220, 15%, 5%, 0.05),
    0 1px 1px hsla(220, 15%, 5%, 0.08);

  /* Niveau 2 : cartes, inputs focalisés */
  --shadow-md:
    0 2px 4px hsla(220, 15%, 5%, 0.06),
    0 4px 8px hsla(220, 15%, 5%, 0.08);

  /* Niveau 3 : dropdowns, tooltips */
  --shadow-lg:
    0 4px 8px hsla(220, 15%, 5%, 0.08),
    0 8px 16px hsla(220, 15%, 5%, 0.12);

  /* Niveau 4 : modales, popovers */
  --shadow-xl:
    0 8px 16px hsla(220, 15%, 5%, 0.10),
    0 16px 32px hsla(220, 15%, 5%, 0.16);
}
```

### Technique des deux ombres
Combiner une ombre directe (petite, nette, peu de blur) et une ombre ambiante (grande, douce, blur élevé) :

```css
box-shadow:
  0 2px 4px rgba(0,0,0,0.12),     /* ombre directe : lumière */
  0 8px 24px rgba(0,0,0,0.08);    /* ombre ambiante : diffuse */
```

L'ombre directe devient presque invisible aux niveaux d'élévation élevés (la modale est si haute que la lumière ambiante l'atteint de partout).

### Ombres et interaction
- Bouton `default` → `--shadow-sm`
- Bouton `hover` → `--shadow-md` (se soulève légèrement)
- Bouton `active/pressed` → `--shadow-none` ou inset (s'enfonce)
- Card `hover` (draggable) → `--shadow-lg` (pop to front)

---

## Profondeur sans ombres (flat design)

### Couleur comme profondeur
- Élément plus clair que le fond → perçu comme surélevé
- Élément plus foncé que le fond → perçu comme en creux

```css
/* Fond de page */
background: hsl(220, 14%, 97%);

/* Card surélevée (plus claire) */
.card { background: hsl(0, 0%, 100%); }

/* Well en creux (plus foncé) */
.well { background: hsl(220, 13%, 93%); }
```

### Ombre solide (flat + profondeur)
```css
/* Ombre sans blur — effet flat mais avec profondeur */
.card-flat {
  box-shadow: 4px 4px 0 hsl(220, 12%, 86%);
}
```

### Overlap (superposition)
Faire se chevaucher des éléments pour créer des couches visuelles :
- Une card qui dépasse de son conteneur parent
- Un avatar qui chevauche deux sections
- Un badge qui sort d'une image

---

## Images dans le layout

### Contrôler le shape des images utilisateur
Ne jamais afficher les images à leur ratio intrinsèque dans un layout structuré. Utiliser des conteneurs fixes avec `object-fit: cover` :

```css
.avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  object-fit: cover;
}
```

### Prévenir le "background bleed"
Quand une image a un fond similaire au fond de la page, utiliser une ombre interne plutôt qu'une bordure :
```css
.user-image {
  box-shadow: inset 0 0 0 1px rgba(0,0,0,0.08);
}
```

### Icons : respecter la taille intentionnelle
Une icône conçue pour 16-24px semblera "chunky" à 64px. Si on a besoin d'une grande icône, l'enfermer dans un conteneur coloré et la garder à sa taille native.

```html
<div class="icon-container">  <!-- 64x64, background coloré, rounded -->
  <svg class="icon">...</svg>   <!-- 20x20, taille native -->
</div>
```