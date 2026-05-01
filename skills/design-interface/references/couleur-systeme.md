# 03 — Système de Couleur

Sources : Refactoring UI ch.4 (Color) · Practical UI ch.3 (Colour)

> **Note :** Ce fichier décrit les concepts stratégiques. Pour les formules mathématiques exactes et la génération programmatique de palettes (JS/CSS), voir `couleur-math.md`.

---

## HSL : le bon format

Utiliser **HSL** (Hue, Saturation, Lightness) pour le web, pas HEX ou RGB.

| Composante | Description | Valeurs |
|---|---|---|
| **Hue** | Position sur la roue chromatique | 0°–360° (0=rouge, 120=vert, 240=bleu) |
| **Saturation** | Intensité de la couleur | 0% (gris) → 100% (vibrant) |
| **Lightness** | Luminosité | 0% (noir) → 50% (pur) → 100% (blanc) |

> Ne pas confondre HSL et HSB. HSB est utilisé dans les outils de design (Figma), HSL est ce que le navigateur comprend. À 100% brightness et 100% saturation en HSB = 100% saturation et 50% lightness en HSL.

---

## Structure d'une palette complète

### Les trois catégories nécessaires

**1. Gris (la majorité de l'interface)**
Textes, fonds, panneaux, bordures, inputs — presque tout est gris.
Prévoir **8-10 nuances**. Trois ou quatre ne suffisent jamais.

```css
--gray-50:  hsl(220, 14%, 97%);
--gray-100: hsl(220, 13%, 93%);
--gray-200: hsl(220, 12%, 86%);
--gray-300: hsl(220, 11%, 74%);
--gray-400: hsl(220, 10%, 60%);
--gray-500: hsl(220, 9%,  46%);
--gray-600: hsl(220, 10%, 36%);
--gray-700: hsl(220, 12%, 26%);
--gray-800: hsl(220, 14%, 16%);
--gray-900: hsl(220, 16%, 8%);
```

**2. Couleur(s) primaire(s)**
La couleur brand. 8-10 nuances également.

**3. Couleurs d'accent (sémantiques)**
Pour les états et les communications système :
- **Rouge** : erreur, action destructive
- **Vert** : succès, positif
- **Jaune/Orange** : avertissement
- **Bleu** : information, lien
- **Couleur brand** : feature en avant, CTA

Chaque couleur d'accent a besoin de **5-10 nuances** aussi.

---

## Créer une nuance de couleur : méthode

### Étape 1 : Choisir la couleur de base
La couleur qui fonctionnerait bien comme fond d'un bouton. Aucune règle de lightness fixe — se fier à l'œil.

### Étape 2 : Trouver les extrêmes
- **Nuance la plus foncée** (900) : pour du texte coloré sur fond blanc
- **Nuance la plus claire** (50-100) : pour des fonds d'alertes ou de tags

### Étape 3 : Remplir les intermédiaires
Nommer les nuances 100 à 900 (ou 50 à 950). 9 niveaux est idéal.
```
50  → ultra-light (fonds d'alertes)
100 → light (fonds de tags)
200 → light-medium
300 → medium-light
400 → medium
500 → base (bouton standard)
600 → medium-dark
700 → dark (hover state)
800 → very-dark (text sur fond coloré)
900 → darkest (titre sur fond coloré)
```

### Attention : la saturation diminue avec la luminosité
Quand un couleur se rapproche de 0% ou 100% de lightness, la saturation semble moins intense. **Augmenter la saturation** pour les nuances très claires et très foncées afin de maintenir la vivacité.

---

## Rotation de teinte pour créer de la profondeur

Plutôt que d'ajuster uniquement la lightness, **faire pivoter la teinte** vers les couleurs intrinsèquement lumineuses/sombres.

- Pour **éclaircir** : pivoter vers 60° (jaune), 180° (cyan), ou 300° (magenta)
- Pour **assombrir** : pivoter vers 0° (rouge), 120° (vert), ou 240° (bleu)

Ne pas dépasser 20-30° de rotation ou la couleur semblera être une autre couleur.

**Exemple pour le jaune :**
Plutôt que d'assombrir en réduisant la lightness (→ marron terne), pivoter la teinte vers l'orange en assombrissant → résultat chaud et riche.

---

## Gris saturés : pas de vrais gris

Les vrais gris (saturation 0%) semblent froids et artificiels. Les gris d'interface sont légèrement saturés.

### Température des gris
- **Gris froids** : teinte bleue (hsl(220, 10-15%, ...))
- **Gris chauds** : teinte orange/jaune (hsl(35, 10-15%, ...))

Maintenir une température cohérente dans toute l'interface. Ne pas mélanger gris froids et chauds sans raison.

---

## Contraste (WCAG 2.1 niveau AA — obligatoire)

| Contexte | Ratio minimum |
|---|---|
| Texte normal < 18px (ou bold < 14px) | **4.5:1** |
| Grand texte ≥ 18px (ou bold ≥ 14px) | **3:1** |
| Composants UI, bordures d'inputs, icônes | **3:1** |
| Texte décoratif, logos, éléments inactifs | Aucune exigence |

### Outils de vérification
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Colour Contrast Analyser](https://www.tpgi.com/color-contrast-checker/)
- Figma Plugin : Stark

---

## Texte sur fond coloré : deux approches

### Approche 1 : Inverser le contraste
Plutôt que texte blanc sur fond coloré foncé (très présent, écrasant) → **texte foncé coloré sur fond coloré très clair**.

```css
/* Alerte information */
background: hsl(220, 80%, 96%);  /* bleu très clair */
color: hsl(220, 60%, 30%);       /* bleu foncé */
```

### Approche 2 : Rotation de teinte pour l'accessibilité
Quand on a du texte coloré sur fond coloré, augmenter le contraste en pivotant la teinte vers une couleur plus lumineuse (jaune, cyan, magenta) plutôt qu'en allant vers le blanc.

---

## Texte sur image de fond : 4 techniques

**1. Overlay semi-transparent**
```css
background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url('image.jpg');
```

**2. Réduire le contraste de l'image**
Baisser le contraste (-30 à -50%) et ajuster la luminosité pour compenser.

**3. Coloriser l'image**
- Réduire le contraste
- Désaturer (grayscale)
- Appliquer un solid fill en mode "multiply"

**4. Text shadow**
```css
text-shadow: 0 0 20px rgba(0,0,0,0.6);  /* glow, pas un vrai shadow */
```

---

## Ne jamais utiliser la couleur seule

La couleur est aveugle aux daltoniens (8% des hommes sont daltoniens rouge-vert).

**Toujours doubler la couleur avec :**
- Une icône (✓ ✗ ⚠)
- Du texte ("Succès", "Erreur", "Attention")
- Une forme ou un motif différent

```html
<!-- Mauvais : couleur seule -->
<span style="color: red">●</span> Erreur

<!-- Bon : couleur + icône -->
<span style="color: red">✗</span> Erreur de validation
```

---

## Appliquer la couleur brand

### 1 couleur brand = tous les éléments interactifs

La couleur brand s'applique à :
- Boutons primaires (fond)
- Liens (texte)
- États focus (outline)
- Checkboxes et radios sélectionnés
- Tabs actifs
- Indicateurs de progression

### Palette de gris : teinter avec la couleur brand
Ajouter une légère teinte de la couleur brand aux gris pour maintenir la cohérence visuelle.
```css
/* Gris légèrement teinté de bleu (brand bleu) */
--gray-500: hsl(220, 9%, 46%);   /* pas hsl(0, 0%, 46%) */
```

---

## Designer en noir et blanc d'abord

Règle systématique : **finaliser le layout, la hiérarchie et l'espacement en grayscale avant d'ajouter de la couleur**.

**Nuance importante :** Concevoir en noir et blanc pour la *structure*, mais s'autoriser la couleur pour l'*état* (Succès, En attente, Erreur) dans des flux complexes où elle agit comme un raccourci cognitif rapide.

Bénéfices :
- Force l'usage de l'espacement et du contraste comme seuls leviers
- Révèle les problèmes de hiérarchie avant qu'ils soient masqués par la couleur
- Produit une interface plus robuste visuellement

---

## Dark Mode : l'avantage du HSL

Grâce à l'utilisation du HSL, créer un Dark Mode est logique, mais **attention : il ne suffit pas de simplement inverser la Lightness**. 

### Règle du HSL Mirroring
Une simple inversion (ex: `100` devient `800`) crée des couleurs trop saturées et agressives sur fond sombre.
Il faut appliquer la méthode du **HSL Mirroring** :
1. **Lightness** : Inverser (un fond très clair devient très sombre).
2. **Saturation** : Réduire de 10% à 30% pour éviter la vibration optique.
3. **Hue (Teinte)** : Décaler légèrement (15-30°) pour un rendu plus riche.

> 👉 Pour les formules de calcul exactes du HSL Mirroring, consultez `couleur-math.md` et les principes d'élévation dans `mode-sombre.md`.

### Couleurs sémantiques en Dark Mode :
Attention : Ne pas inverser les couleurs sémantiques (succès, erreur, brand) de la même façon que les surfaces. Un bouton primaire doit rester identifiable (souvent autour de 500-600 en lightness).
- Assombrir légèrement les fonds d'alertes.
- Garder les textes d'alerte lisibles en augmentant leur lightness.