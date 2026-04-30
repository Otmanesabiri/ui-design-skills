# 07 — Composants UI

Sources : Refactoring UI · Practical UI ch.6 (Forms) · Laws of UX (Fitts, Hick)

---

## Boutons

### Anatomie d'un bon bouton

```css
.btn-primary {
  /* Structure */
  display: inline-flex;
  align-items: center;
  gap: 8px;

  /* Sizing */
  padding: 10px 20px;
  min-height: 44px;       /* WCAG touch target */
  border-radius: 6px;

  /* Typographie */
  font-size: 14px;
  font-weight: 600;
  line-height: 1.2;
  white-space: nowrap;

  /* Couleur */
  background: var(--color-primary-500);
  color: #fff;
  border: none;

  /* Interaction */
  cursor: pointer;
  transition: background 150ms ease, box-shadow 150ms ease;
}
```

### Tous les états (obligatoires)

| État | Modification |
|------|-------------|
| `default` | Couleur base, shadow sm |
| `hover` | Couleur -100 (plus foncée), shadow md |
| `focus` | Outline 2px couleur brand, offset 2px |
| `active` | Couleur -200, shadow none (s'enfonce) |
| `disabled` | Opacité 0.5, cursor not-allowed, pointer-events none |
| `loading` | Spinner + texte "..." ou maintenir le texte original |

### Taille des boutons

| Taille | Padding | Font-size | Usage |
|--------|---------|-----------|-------|
| xs | 4px 10px | 12px | Actions dans des tables ou espaces compacts |
| sm | 6px 14px | 13px | Actions secondaires inline |
| md | 10px 20px | 14px | Bouton standard |
| lg | 14px 28px | 16px | CTA principal, formulaires |
| xl | 18px 36px | 18px | Hero CTA |

### Texte du bouton
- **Verbe d'action précis** : "Créer un compte", "Envoyer le rapport", "Supprimer le fichier"
- **Pas** : "OK", "Submit", "Confirmer" (trop vague)
- **Capitalisation** : Sentence case de préférence ("Envoyer"), pas ALL CAPS

---

## Formulaires

### Structure d'un formulaire

**Ordre optimal des éléments :**
```
1. Titre/contexte (pourquoi ce formulaire)
2. Champs regroupés par thème
3. Helper text sous les champs complexes
4. Validation inline immédiate
5. Bouton de soumission (seul, primaire, en bas à droite)
6. Lien/action secondaire (annuler, revenir) à gauche
```

### Labels

```css
/* Toujours au-dessus du champ, pas à gauche (sauf cas spéciaux) */
.label {
  display: block;
  font-size: 14px;
  font-weight: 500;
  color: hsl(220, 10%, 35%);
  margin-bottom: 6px;
}
```

**Eviter les placeholders comme seuls labels** — ils disparaissent dès que l'utilisateur commence à taper.

### Champs de saisie (inputs)

```css
.input {
  width: 100%;
  padding: 10px 14px;
  font-size: 16px;         /* ≥16px sur iOS pour éviter le zoom automatique */
  border: 1.5px solid hsl(220, 12%, 80%);
  border-radius: 6px;
  background: #fff;
  transition: border-color 150ms;
}

.input:focus {
  outline: none;
  border-color: var(--color-primary-500);
  box-shadow: 0 0 0 3px hsla(var(--color-primary-hsl), 0.15);
}

.input.error {
  border-color: hsl(0, 70%, 55%);
}

.input:disabled {
  background: hsl(220, 13%, 96%);
  cursor: not-allowed;
  opacity: 0.7;
}
```

### Validation et erreurs

**Timing de validation :**
- Valider **au blur** (quand l'utilisateur quitte le champ), pas au keystroke
- Exception : feedback positif (✓) peut apparaître en temps réel une fois la valeur valide

**Message d'erreur :**
```html
<div class="field">
  <label for="email">Email</label>
  <input id="email" type="email" aria-describedby="email-error" />
  <p id="email-error" class="error-message" role="alert">
    ✗ Veuillez entrer une adresse email valide
  </p>
</div>
```

```css
.error-message {
  font-size: 13px;
  color: hsl(0, 70%, 50%);
  margin-top: 4px;
  display: flex;
  align-items: center;
  gap: 4px;
}
```

### Formulaires multi-étapes (Hick's Law)

```
Step 1/4 ─────────────────────
Informations personnelles
  Prénom    Nom
  Email
  
               [Continuer →]
```

**Règles :**
- Afficher le numéro d'étape et le total (`Étape 2 sur 4`)
- Regrouper les champs liés dans la même étape
- Permettre le retour en arrière sans perdre les données
- Bouton "Continuer" uniquement, pas de "Sauvegarder" prématuré

### Champs optionnels

Éviter les champs optionnels. Utiliser des **opt-in progressifs** :

```
// MAUVAIS
[Téléphone (optionnel)]

// BON
□ Recevoir des mises à jour par SMS
  Si oui → [Téléphone] (champ revealed dynamiquement)
```

### Attributs HTML importants

```html
<!-- Toujours spécifier autocomplete pour les champs communs -->
<input type="email" autocomplete="email" />
<input type="tel" autocomplete="tel" />
<input type="text" autocomplete="given-name" />

<!-- inputmode pour le clavier mobile adapté -->
<input type="text" inputmode="numeric" />    <!-- chiffres uniquement -->
<input type="text" inputmode="decimal" />    <!-- chiffres + virgule -->
<input type="text" inputmode="tel" />        <!-- clavier téléphone -->
<input type="text" inputmode="email" />      <!-- clavier email (@, .) -->
```

---

## Tables de données et Composants Complexes

Pour les vues très denses (Dashboards, Tables avec >10 colonnes), appliquer la **Loi de Miller** : l'humain ne peut traiter que ~7 éléments à la fois. La solution est le *Chunking* (regroupement visuel).

### Chunking (Regroupement) dans les Tables
Au lieu d'ajouter une colonne par donnée, fusionnez les données liées :
```html
<!-- AVANT : 3 colonnes (Avatar | Nom | Email) -->

<!-- APRÈS : 1 colonne (Utilisateur) -->
<td class="user-cell">
  <img src="avatar.jpg" class="avatar" />
  <div class="user-info">
    <span class="name">Jane Doe</span>
    <span class="email text-secondary">jane@example.com</span>
  </div>
</td>
```

### Alignement

| Type de donnée | Alignement |
|---|---|
| Texte, Utilisateurs, Liens | Gauche |
| Nombres, montants, dates | **Droite** (facilite la comparaison visuelle) |
| Status, badges, icônes | Centre |
| Actions (boutons, menu `...`) | Centre ou droite |
| Checkboxes de sélection | Centre |

### Gestion de la Complexité (Scroll & Filtres)
- **Scroll horizontal :** Fixez (`position: sticky`) toujours la première colonne (l'identifiant clé) et le header de la table.
- **Filtres :** Ne montrez pas 10 champs de filtres vides. Utilisez un bouton "Filtrer" qui ouvre un Popover/Drawer. Affichez les filtres actifs sous forme de "Tags" amovibles au-dessus de la table.
- **Bulk Actions :** La barre d'actions groupées (Supprimer, Exporter) ne doit apparaître que lorsqu'au moins une ligne est sélectionnée, remplaçant souvent le header de la table ou flottant en bas de l'écran.

### Structure CSS recommandée

```css
/* En-têtes */
th {
  font-size: 12px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: hsl(220, 10%, 55%);
  padding: 12px 16px;
  background: hsl(220, 14%, 97%);
  border-bottom: 1px solid hsl(220, 12%, 88%);
}

/* Lignes */
td {
  padding: 14px 16px;
  font-size: 14px;
  border-bottom: 1px solid hsl(220, 12%, 93%);
}

/* Hover sur une ligne */
tr:hover td {
  background: hsl(220, 14%, 98%);
}
```

### Tri des colonnes

Indiquer la colonne triée et sa direction :
```html
<th aria-sort="ascending">
  Montant <svg class="sort-icon">↑</svg>
</th>
```

---

## Modales

### Anatomie

```
┌──────────────────────────────────┐
│ Titre de la modale          [×]  │  ← Header
├──────────────────────────────────┤
│                                  │
│  Contenu / question              │  ← Body (scrollable si long)
│                                  │
├──────────────────────────────────┤
│ [Action secondaire]  [Primaire]  │  ← Footer, actions à droite
└──────────────────────────────────┘
```

**Règles :**
- Une modale = une seule décision ou action
- Toujours 3 façons de fermer : bouton ×, clic overlay, touche Echap
- Bloquer le scroll du fond quand la modale est ouverte (`body: overflow: hidden`)
- Focus trap : la navigation clavier reste dans la modale
- Ombre forte (`--shadow-xl`) pour signaler l'élévation

### Overlay

```css
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(2px);   /* optionnel, attention performance */
  z-index: 100;
}
```

---

## États d'interface

### État vide (Empty State)

Ne jamais laisser un espace blanc avec juste "Aucun résultat". Guider l'utilisateur.

```
     [Illustration ou icône]
     
     Vous n'avez pas encore de projets
     
     Commencez par créer votre premier projet
     pour organiser vos tâches.
     
         [Créer un projet]
```

**Composants :**
- Illustration (optionnelle mais efficace)
- Titre descriptif
- Message d'explication
- Action principale (bouton)

### État de chargement

| Durée estimée | Solution recommandée |
|---|---|
| < 300ms | Rien (assez rapide) |
| 300ms – 1s | Spinner discret |
| 1s – 3s | Skeleton screen |
| > 3s | Skeleton + texte d'état + % si possible |

**Skeleton screen :**
```css
.skeleton {
  background: linear-gradient(
    90deg,
    hsl(220, 13%, 93%) 25%,
    hsl(220, 13%, 90%) 50%,
    hsl(220, 13%, 93%) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: 4px;
}

@keyframes shimmer {
  0%   { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

### État d'erreur

**Structure d'un bon message d'erreur :**
1. Ce qui s'est passé (sans jargon technique)
2. Pourquoi ça s'est passé (si pertinent)
3. Comment y remédier (action concrète)

```
✗ Connexion impossible

Votre session a expiré. Cela arrive après 30 minutes d'inactivité.

[Se reconnecter]  ou  Contacter le support
```

**Ne jamais afficher :**
- `Error 500`
- `Network error: ECONNREFUSED`
- `Null pointer exception`

### État de succès

```css
.toast-success {
  background: hsl(142, 70%, 96%);
  border: 1px solid hsl(142, 60%, 80%);
  color: hsl(142, 60%, 25%);
  padding: 12px 16px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  gap: 10px;
}
```

---

## Notifications & Toasts

### Durée d'affichage recommandée
- Toast informatif : **3-4 secondes**
- Toast avec action (Annuler) : **6-8 secondes**
- Toast d'erreur : **persistant jusqu'à fermeture manuelle**

### Position
- Desktop : coin en bas à droite ou en bas au centre
- Mobile : en bas, au-dessus de la navigation

### Accessibilité
```html
<div role="status" aria-live="polite">     <!-- pour les infos -->
<div role="alert" aria-live="assertive">   <!-- pour les erreurs -->
```