# 18 — Data Visualization

Sources : Refactoring UI · Practical UI · Laws of UX (Miller, Von Restorff)

---

## Choisir le bon type de graphique

| Objectif | Graphique recommandé | À éviter |
|----------|---------------------|----------|
| Évolution dans le temps | Line chart, Area chart | Pie chart |
| Comparaison entre catégories | Bar chart (horizontal) | 3D charts |
| Proportion d'un tout | Donut chart (≤ 5 segments) | Pie chart > 5 segments |
| Corrélation entre deux variables | Scatter plot | Bar chart |
| Distribution de données | Histogram | Line chart |
| Données tabulaires structurées | Table | Tout graphique |
| KPI unique | Stat card + sparkline | Graphique complexe |

### Règle de Miller : ≤ 5-7 catégories par graphique

Au-delà de 7 séries ou segments, la mémoire de travail est saturée. Regrouper les catégories mineures sous "Autres".

---

## Couleurs catégorielles pour daltoniens

### Le problème

Les palettes classiques utilisent rouge + vert pour différencier les catégories — exactement les couleurs invisibles pour les 8% d'hommes daltoniens rouge-vert (deuteranopie).

### Palettes sûres

**Palette 4 couleurs (universelle)**
```css
:root {
  --chart-1: hsl(211, 80%, 50%);   /* bleu */
  --chart-2: hsl(27,  90%, 55%);   /* orange */
  --chart-3: hsl(145, 55%, 40%);   /* vert foncé */
  --chart-4: hsl(280, 60%, 55%);   /* violet */
}
```

**Palette 6 couleurs (testée daltonisme)**
```css
:root {
  --chart-1: hsl(211, 80%, 50%);   /* bleu */
  --chart-2: hsl(27,  90%, 55%);   /* orange */
  --chart-3: hsl(145, 55%, 40%);   /* vert foncé */
  --chart-4: hsl(340, 75%, 55%);   /* rose/magenta */
  --chart-5: hsl(50,  95%, 50%);   /* jaune */
  --chart-6: hsl(195, 70%, 45%);   /* cyan foncé */
}
```

**Palette séquentielle (une variable, intensité croissante)**
```css
/* Pour des données quantitatives (ex: température, densité) */
:root {
  --seq-1: hsl(220, 70%, 95%);  /* très clair */
  --seq-2: hsl(220, 70%, 80%);
  --seq-3: hsl(220, 70%, 60%);
  --seq-4: hsl(220, 70%, 45%);
  --seq-5: hsl(220, 70%, 28%);  /* très foncé */
}
```

### Toujours doubler la couleur

```html
<!-- MAUVAIS : couleur seule -->
<li style="color: red">● Catégorie A</li>
<li style="color: green">● Catégorie B</li>

<!-- BON : couleur + forme + label -->
<li>
  <span class="legend-dot" style="background: var(--chart-1)"></span>
  <span class="legend-pattern legend-circle"></span>
  Catégorie A
</li>
<li>
  <span class="legend-dot" style="background: var(--chart-2)"></span>
  <span class="legend-pattern legend-square"></span>
  Catégorie B
</li>
```

---

## KPI Cards (Stat Cards)

Structure recommandée pour les tableaux de bord.

```html
<div class="kpi-card">
  <div class="kpi-header">
    <span class="kpi-label">Revenus ce mois</span>
    <svg class="kpi-icon" aria-hidden="true"><!-- icône --></svg>
  </div>

  <div class="kpi-value">
    <span class="kpi-number">24 500</span>
    <span class="kpi-unit">€</span>
  </div>

  <div class="kpi-trend" aria-label="En hausse de 12% vs mois précédent">
    <svg aria-hidden="true"><!-- flèche ↑ --></svg>
    <span class="trend-value trend-positive">+12%</span>
    <span class="trend-period">vs mois précédent</span>
  </div>

  <!-- Sparkline optionnel -->
  <div class="kpi-sparkline" aria-hidden="true">
    <!-- Mini graphique, décoratif uniquement -->
  </div>
</div>
```

```css
.kpi-card {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border-subtle);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  box-shadow: var(--shadow-sm);
}

.kpi-label {
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--color-text-secondary);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.kpi-number {
  font-size: var(--text-4xl);
  font-weight: 700;
  color: var(--color-text-primary);
  font-variant-numeric: tabular-nums;  /* chiffres à largeur fixe */
}

.trend-positive { color: var(--success-600); }
.trend-negative { color: var(--error-600); }
```

---

## Tables de données denses

### Densité selon le contexte

```css
/* Compact — dashboards, listes d'audit */
.table-compact td { padding: 8px 12px; font-size: 13px; }

/* Standard — usage général */
.table-standard td { padding: 12px 16px; font-size: 14px; }

/* Comfortable — lecture approfondie */
.table-comfortable td { padding: 16px 20px; font-size: 15px; }
```

### Alignement des données (rappel)

```css
/* Chiffres et montants → droite (décimales alignées) */
td.numeric {
  text-align: right;
  font-variant-numeric: tabular-nums;  /* empêche les colonnes de "danser" */
}

/* Texte → gauche */
td.text { text-align: left; }

/* Statuts, badges → centre */
td.status { text-align: center; }
```

### Colonnes fixes pour les grandes tables

```css
/* Figer la première colonne (identifiant) */
.table-sticky th:first-child,
.table-sticky td:first-child {
  position: sticky;
  left: 0;
  background: var(--color-bg-card);
  z-index: 1;
  box-shadow: 2px 0 4px rgba(0,0,0,0.06);  /* séparation visuelle */
}

/* Figer le header */
.table-sticky thead th {
  position: sticky;
  top: 0;
  background: var(--color-bg-card);
  z-index: 2;
}

/* Coin figé (header + première colonne) */
.table-sticky thead th:first-child {
  z-index: 3;
}
```

### Pagination vs infinite scroll

| Contexte | Recommandation |
|----------|---------------|
| Données que l'utilisateur parcourt dans l'ordre | Infinite scroll |
| Données que l'utilisateur cherche (avec filtres) | Pagination |
| Export ou traitement des données | Pagination obligatoire |
| Mobile | Infinite scroll avec bouton "Charger plus" |

---

## Axes et labels de graphiques

### Règles des axes

```
Axe Y (vertical)
- Commencer à 0 pour les bar charts (sinon manipulation visuelle)
- Exception : line charts comparatifs — can tronquer si clairement indiqué
- Labels : côté gauche, horizontaux (jamais verticaux)
- Nombre de graduations : 4-6 maximum

Axe X (horizontal)
- Dates : format cohérent (Jan, Fév, Mar ou 01/24, 02/24)
- Labels longs : rotation 45° ou format court
- Espacer pour éviter la surcharge
```

### Grilles de fond

```css
/* Grille légère — guide sans distraire */
.chart-grid line {
  stroke: var(--gray-200);
  stroke-dasharray: 4 4;
  stroke-width: 1;
}

/* Pas de grille verticale sur les line charts (bruit inutile) */
/* Grille horizontale uniquement */
```

---

## États des graphiques

### Loading state

```html
<!-- Skeleton pour graphique -->
<div class="chart-skeleton" aria-busy="true" aria-label="Graphique en chargement">
  <div class="skeleton chart-bar" style="height: 60%"></div>
  <div class="skeleton chart-bar" style="height: 80%"></div>
  <div class="skeleton chart-bar" style="height: 45%"></div>
  <div class="skeleton chart-bar" style="height: 90%"></div>
</div>
```

### Empty state (données nulles)

```html
<div class="chart-empty">
  <svg><!-- Icône graphique vide --></svg>
  <p>Aucune donnée pour cette période</p>
  <button>Modifier les filtres</button>
</div>
```

### Erreur de chargement

```html
<div class="chart-error" role="alert">
  <svg><!-- Icône erreur --></svg>
  <p>Impossible de charger les données</p>
  <button onclick="retry()">Réessayer</button>
</div>
```

---

## Accessibilité des graphiques

```html
<!-- Toujours fournir une alternative textuelle -->
<figure>
  <figcaption>
    Évolution des revenus mensuels de janvier à juin 2025.
    Pic en avril à 32 500€, baisse en mai à 28 000€.
  </figcaption>
  <div class="chart-container" aria-hidden="true">
    <!-- SVG graphique -->
  </div>
  <!-- Table des données accessible -->
  <details>
    <summary>Voir les données en tableau</summary>
    <table>
      <thead><tr><th>Mois</th><th>Revenus</th></tr></thead>
      <tbody>
        <tr><td>Janvier</td><td>24 500 €</td></tr>
        <!-- ... -->
      </tbody>
    </table>
  </details>
</figure>
```

---

## Checklist Data Viz

```
Choix du graphique
[ ] Type adapté à l'objectif (comparaison, évolution, proportion)
[ ] ≤ 7 catégories ou séries visibles simultanément
[ ] Pas de 3D (illusion de profondeur = distorsion des données)

Couleurs
[ ] Palette testée pour le daltonisme
[ ] Couleur doublée avec forme ou texture
[ ] Couleurs sémantiques cohérentes (rouge = mauvais, vert = bon)

Tables
[ ] Chiffres alignés à droite avec tabular-nums
[ ] Colonnes figées si table scrollable
[ ] Tri actif indiqué visuellement

Accessibilité
[ ] Alternative textuelle (figcaption)
[ ] Données disponibles en table
[ ] États loading/empty/error conçus

Performance
[ ] Virtualisation si > 1000 lignes
[ ] Données agrégées côté serveur (pas côté client)
```
