# 16 — Accessibilité Avancée (Au-delà des Couleurs)

Sources : WCAG 2.1 · WAI-ARIA 1.2 · Practical UI (Dannaway) · Laws of UX (Postel's Law)

> Le fichier `03-couleur.md` couvre le contraste et la règle "couleur seule insuffisante".
> Ce fichier couvre tout le reste : clavier, sémantique HTML, ARIA, motion.

---

## Navigation au clavier

### focus-visible vs focus vs hover : 3 états distincts

```css
/* MAUVAIS : supprimer le focus (erreur fréquente) */
*:focus { outline: none; }

/* BON : utiliser :focus-visible */
*:focus-visible {
  outline: 3px solid var(--color-brand);
  outline-offset: 3px;
  border-radius: 4px;
}

/* Les états hover et focus-visible doivent être visuellement différents */
.btn:hover       { background: var(--blue-600); }
.btn:focus-visible {
  background: var(--blue-500);
  outline: 3px solid var(--blue-300);
  outline-offset: 3px;
}
```

### Ordre de tabulation logique

```html
<!-- L'ordre du DOM = ordre de tabulation -->
<!-- Structurer le HTML dans l'ordre de lecture logique -->

<!-- MAUVAIS : navigation visuelle ≠ DOM order -->
<div style="display: flex; flex-direction: row-reverse;">
  <button>Action secondaire</button>  <!-- visuellement à droite -->
  <button>Action principale</button>  <!-- visuellement à gauche -->
</div>

<!-- BON : DOM order = ordre naturel -->
<div style="display: flex;">
  <button>Action principale</button>
  <button>Action secondaire</button>
</div>
```

### tabindex : règles d'usage

```html
<!-- tabindex="0" : inclure dans l'ordre naturel -->
<div role="button" tabindex="0">Bouton custom</div>

<!-- tabindex="-1" : focusable par JS mais pas au clavier -->
<div id="modal-content" tabindex="-1">...</div>

<!-- tabindex="1+" : NE JAMAIS UTILISER -->
<!-- Casse l'ordre naturel et crée des bugs de navigation -->
```

### Focus trap dans les modales

```javascript
function trapFocus(element) {
  const focusableSelectors = [
    'a[href]', 'button:not([disabled])',
    'input:not([disabled])', 'select:not([disabled])',
    'textarea:not([disabled])', '[tabindex="0"]'
  ].join(', ');

  const focusables = [...element.querySelectorAll(focusableSelectors)];
  const first = focusables[0];
  const last = focusables[focusables.length - 1];

  element.addEventListener('keydown', (e) => {
    if (e.key !== 'Tab') return;

    if (e.shiftKey) {
      if (document.activeElement === first) {
        e.preventDefault();
        last.focus();
      }
    } else {
      if (document.activeElement === last) {
        e.preventDefault();
        first.focus();
      }
    }
  });

  first.focus(); // focus initial sur ouverture
}
```

---

## Sémantique HTML

### Règle fondamentale : 1 seul H1 par page

```html
<!-- Structure correcte des headings -->
<h1>Titre principal de la page</h1>      <!-- 1 seul -->
  <h2>Section principale</h2>
    <h3>Sous-section</h3>
    <h3>Sous-section</h3>
  <h2>Section suivante</h2>
    <h3>Sous-section</h3>

<!-- JAMAIS sauter des niveaux -->
<!-- MAUVAIS : h1 → h3 (h2 manquant) -->
<!-- BON : h1 → h2 → h3 (séquence continue) -->
```

### Éléments sémantiques vs div

```html
<!-- MAUVAIS : divs partout -->
<div class="header">
  <div class="nav">...</div>
</div>
<div class="main">
  <div class="article">...</div>
  <div class="aside">...</div>
</div>
<div class="footer">...</div>

<!-- BON : éléments sémantiques -->
<header>
  <nav aria-label="Navigation principale">...</nav>
</header>
<main>
  <article>...</article>
  <aside aria-label="Informations complémentaires">...</aside>
</main>
<footer>...</footer>
```

### Boutons vs Liens : distinction critique

```html
<!-- Lien : navigue vers une URL -->
<a href="/dashboard">Tableau de bord</a>

<!-- Bouton : déclenche une action -->
<button type="button" onclick="openModal()">Ouvrir</button>

<!-- MAUVAIS : div ou span comme bouton -->
<div onclick="submit()">Envoyer</div>
<!-- Pas de focus clavier, pas de role, pas d'événement Enter/Space -->

<!-- BON : vrai bouton -->
<button type="submit">Envoyer</button>
```

---

## Attributs ARIA

### Règle n°1 : préférer le HTML sémantique à ARIA

```
Priorité 1 → Élément HTML natif (button, input, nav...)
Priorité 2 → ARIA uniquement quand le HTML natif ne suffit pas
```

### Icônes : aria-hidden et aria-label

```html
<!-- Icône décorative (accompagne du texte) → masquer aux screen readers -->
<button>
  <svg aria-hidden="true" focusable="false">...</svg>
  Envoyer
</button>

<!-- Icône seule (sans texte) → label obligatoire -->
<button aria-label="Fermer la modal">
  <svg aria-hidden="true" focusable="false">...</svg>
</button>

<!-- Icône avec signification (status) → role + label -->
<span role="img" aria-label="Succès">✓</span>
```

### États dynamiques

```html
<!-- Dropdown / Menu -->
<button aria-expanded="false" aria-controls="menu-id">
  Options
</button>
<ul id="menu-id" role="menu" hidden>...</ul>

<!-- Changer aria-expanded en JS -->
button.setAttribute('aria-expanded', 'true');
menu.removeAttribute('hidden');

<!-- Loading state -->
<button aria-busy="true" aria-label="Chargement en cours...">
  <span aria-hidden="true">Enregistrer</span>
</button>

<!-- Erreur de formulaire -->
<input
  id="email"
  aria-describedby="email-error"
  aria-invalid="true"
/>
<p id="email-error" role="alert">
  Adresse email invalide
</p>
```

### Live regions : annonces dynamiques

```html
<!-- Annonces polies (attend la fin de l'action utilisateur) -->
<div aria-live="polite" aria-atomic="true" class="sr-only">
  <!-- Injecter ici les messages de statut dynamiques -->
</div>

<!-- Annonces urgentes (interrompt immédiatement) -->
<div role="alert" aria-live="assertive">
  <!-- Erreurs critiques uniquement -->
</div>
```

```css
/* Classe visually-hidden : masqué visuellement, lisible par screen readers */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

---

## Skip links

Permettre aux utilisateurs clavier de passer directement au contenu principal.

```html
<!-- Premier élément focusable de la page -->
<a href="#main-content" class="skip-link">
  Aller au contenu principal
</a>

<header>...</header>
<main id="main-content" tabindex="-1">...</main>
```

```css
.skip-link {
  position: absolute;
  top: -100%;
  left: 0;
  background: var(--color-brand);
  color: white;
  padding: 12px 20px;
  z-index: var(--z-top);
  border-radius: 0 0 8px 0;
  font-weight: 600;
  text-decoration: none;
}

.skip-link:focus {
  top: 0;  /* Apparaît uniquement au focus clavier */
}
```

---

## Reduced Motion

Certains utilisateurs souffrent de troubles vestibulaires — les animations peuvent causer des nausées ou des crises.

```css
/* Appliquer à toutes les animations */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

/* Pattern recommandé : opt-in plutôt qu'opt-out */
@media (prefers-reduced-motion: no-preference) {
  .animated-element {
    transition: transform 300ms var(--ease-spring);
  }
}
```

```javascript
// Vérifier en JS avant de lancer une animation
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

if (!prefersReducedMotion) {
  element.animate([...], { duration: 300 });
} else {
  // Changement immédiat sans animation
  element.style.opacity = 1;
}
```

---

## Tailles touch et zones cliquables

```css
/* Minimum recommandé : 44×44px (Apple HIG, WCAG 2.5.5) */
.interactive-element {
  min-width: 44px;
  min-height: 44px;
}

/* Si l'élément est visuellement plus petit, agrandir la zone de click */
.small-icon-btn {
  width: 24px;
  height: 24px;
  padding: 10px;  /* zone réelle = 44px */
  margin: -10px;  /* compenser le padding pour le layout */
}
```

---

## Checklist accessibilité rapide

```
Clavier
[ ] Tous les éléments interactifs accessibles au clavier
[ ] focus-visible visible et distinct du hover
[ ] Ordre de tabulation logique (= ordre DOM)
[ ] Focus trap dans les modales/drawers
[ ] Skip link présent

Sémantique
[ ] 1 seul H1 par page
[ ] Hiérarchie des headings continue (pas de sauts)
[ ] Éléments sémantiques utilisés (nav, main, article, aside...)
[ ] Boutons pour les actions, liens pour la navigation

ARIA
[ ] Icônes décoratives avec aria-hidden="true"
[ ] Icônes seules avec aria-label
[ ] États dynamiques (aria-expanded, aria-invalid, aria-busy)
[ ] Live regions pour les mises à jour dynamiques

Motion
[ ] prefers-reduced-motion respecté
[ ] Aucune animation indispensable à la compréhension

Touch
[ ] Zones touch ≥ 44×44px sur mobile
```
