# Exemple : Génération d'un Dashboard

**Requête de l'utilisateur :** "Génère-moi une structure pour un dashboard SaaS avec une vue d'ensemble des revenus, des utilisateurs actifs et un tableau des dernières transactions."

## Réponse de l'Agent (Basée sur les UI Skills)

### 1. Analyse et Hiérarchie (Grayscale First)
Avant d'appliquer des couleurs, nous structurons la vue pour prioriser l'information :
1. **Titres et Actions Globales :** En haut (H1 + Bouton d'export).
2. **Kpis (Key Performance Indicators) :** Les métriques clés en haut pour une visibilité immédiate.
3. **Tableau des Transactions :** En dessous, détaillé mais aéré.

### 2. Application des Tokens
- **Espacement :** Utilisation de `gap-6` (24px) entre les grandes sections et `gap-4` (16px) à l'intérieur des cartes.
- **Typographie :** Les valeurs des KPIs utilisent une police large (ex: `text-3xl`, `font-bold`), le texte secondaire est `text-sm` avec une couleur `color-text-secondary`.
- **Surfaces :** Le fond principal est `color-bg-page`, les cartes sont sur `color-bg-card` avec une ombre douce `shadow-sm` pour créer de l'élévation.

### 3. Résultat (Structure HTML/CSS ou Composant)
```html
<div class="dashboard-layout" style="background: var(--color-bg-page); padding: var(--space-8);">
  <header style="display: flex; justify-content: space-between; margin-bottom: var(--space-8);">
    <h1 style="font-size: var(--text-2xl); font-weight: 700; color: var(--color-text-primary);">Vue d'ensemble</h1>
    <button style="background: var(--color-brand); color: var(--color-text-inverse); padding: var(--space-2) var(--space-4); border-radius: var(--radius-md);">
      Exporter le rapport
    </button>
  </header>
  
  <section class="kpi-grid" style="display: grid; grid-template-columns: repeat(3, 1fr); gap: var(--space-6); margin-bottom: var(--space-8);">
    <div class="kpi-card" style="background: var(--color-bg-card); padding: var(--space-6); border-radius: var(--radius-lg); box-shadow: var(--shadow-sm);">
      <span style="color: var(--color-text-secondary); font-size: var(--text-sm);">Revenus Totaux</span>
      <p style="color: var(--color-text-primary); font-size: var(--text-3xl); font-weight: 800; margin-top: var(--space-2);">$24,500</p>
    </div>
    <!-- Autres KPIs... -->
  </section>
  
  <!-- Section Tableau... -->
</div>
```

**Justification UX :**
- **Loi de Hick :** Le nombre d'actions globales est limité à une seule (Exporter).
- **Chunking :** Les statistiques sont regroupées dans des cartes distinctes pour une lecture facile.

### 4. Résultat Attendu 👁️
Visuellement, cela produit une page aérée avec un fond gris très clair (`--color-bg-page`). Le titre de la page est bien visible, tout comme le bouton d'action primaire en couleur de marque (`--color-brand`). En dessous, trois cartes blanches (`--color-bg-card`) aux coins arrondis se détachent subtilement grâce à une légère ombre, contenant chacune un indicateur chiffré proéminent et lisible.
