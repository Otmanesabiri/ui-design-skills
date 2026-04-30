# 06 — Lois UX (Psychologie Appliquée)

Source : Laws of UX 2e éd. — Jon Yablonski

---

## Vue d'ensemble

| Loi | Principe en une phrase | Impact principal |
|-----|----------------------|-----------------|
| Jakob's Law | Les utilisateurs préfèrent ce qui ressemble à ce qu'ils connaissent | Navigation, patterns |
| Fitts's Law | Plus c'est grand et proche, plus c'est facile à atteindre | Taille et position des cibles |
| Miller's Law | La mémoire de travail est limitée à ~7 éléments | Groupement, progressive disclosure |
| Hick's Law | Plus il y a de choix, plus la décision est lente | Simplification des options |
| Postel's Law | Être strict dans ce qu'on produit, flexible dans ce qu'on accepte | Robustesse, accessibilité |
| Peak-End Rule | On juge une expérience par son pic et sa fin | Onboarding, confirmation, erreur |
| Aesthetic-Usability Effect | Les interfaces belles semblent plus faciles | Qualité visuelle et confiance |
| Von Restorff Effect | Ce qui diffère est mémorisé | Mise en valeur des éléments clés |
| Tesler's Law | La complexité est incompressible, elle se déplace | Simplification UX vs complexité backend |
| Doherty Threshold | Productivité max sous 400ms de latence | Performance perçue, feedback |

---

## 1. Jakob's Law

> "Les utilisateurs passent la plupart de leur temps sur d'autres sites. Ils préfèrent que votre site fonctionne comme tous les autres qu'ils connaissent déjà."
>
> — Jakob Nielsen, 2000

### Principe
Les utilisateurs construisent des modèles mentaux de comment les interfaces fonctionnent à partir de leur expérience accumulée. Quand une nouvelle interface respecte ces modèles, la courbe d'apprentissage est quasi nulle.

### Applications concrètes
- Logo en haut à gauche → cliquable vers l'accueil
- Navigation principale en haut ou à gauche
- Bouton de fermeture (×) en haut à droite des modales
- Champ de recherche avec icône loupe
- Fil d'Ariane pour la navigation hiérarchique
- Icône panier pour le e-commerce

### Quand innover
Innover sur le **contenu**, pas sur les **patterns d'interaction**. La rupture avec les conventions coûte de l'énergie cognitive à l'utilisateur. Ce coût doit être justifié par une valeur réelle.

### Erreur fréquente
Créer une navigation non-conventionnelle pour se différencier. L'utilisateur veut accomplir une tâche, pas apprendre une nouvelle navigation.

---

## 2. Fitts's Law

> "Le temps pour atteindre une cible est une fonction de la distance et de la taille de cette cible."
>
> — Paul Fitts, 1954

### Formule simplifiée
Plus la cible est **grande** et **proche** du point de départ, moins de temps il faut pour l'atteindre.

### Applications concrètes

**Taille des cibles touch (mobile)**
Taille minimum recommandée : **44 × 44px** (Apple HIG, WCAG 2.5.5 niveau AAA : 44×44px, niveau AA : 24×24px)
```css
.btn {
  min-width: 44px;
  min-height: 44px;
}
```

**Actions fréquentes → en bas de l'écran sur mobile**
La zone naturelle du pouce est en bas de l'écran. Les actions primaires (CTA, tab bar) doivent s'y trouver.

**Éviter les actions dangereuses proches des actions courantes**
Ne pas placer "Supprimer" à côté de "Sauvegarder" sans espace suffisant.

**Bords et coins d'écran**
Les bords et coins de l'écran sont des "cibles infiniment grandes" (le curseur s'y arrête naturellement). Les menus macOS en haut de l'écran exploitent ça.

### Erreur fréquente
Mettre "Accepter" et "Refuser" côte à côte en petite taille dans une dialog. L'utilisateur doit lever son pouce ou zoomer pour sélectionner le bon bouton.

---

## 3. Miller's Law

> "La personne moyenne peut garder 7 (±2) éléments en mémoire de travail."
>
> — George Miller, 1956

### Ce que cette loi ne dit pas
Miller's Law ne dit **pas** que la navigation doit être limitée à 7 items. Utiliser ce chiffre comme limite stricte est une mauvaise application de la loi.

### Ce qu'elle dit vraiment
La mémoire de travail est limitée. Les informations trop nombreuses ou trop denses créent une surcharge cognitive.

### Applications concrètes
- **Chunking** : regrouper les informations en blocs logiques (ex: numéros de téléphone `06 12 34 56 78` et non `0612345678`)
- **Progressive disclosure** : révéler l'information graduellement
- **Formulaires multi-étapes** : découper les longs formulaires

### La taille réelle de la mémoire de travail
Les recherches plus récentes (Cowan, 2001) suggèrent plutôt **4 éléments** comme limite. Miller's Law est moins précise qu'on ne le croit.

---

## 4. Hick's Law

> "Le temps de prise de décision augmente avec le nombre et la complexité des choix disponibles."
>
> — Hick & Hyman, 1952

### Formule
`T = b × log₂(n + 1)` — le temps de décision est logarithmique, pas linéaire.

### Applications concrètes

**Réduire les options visibles**
Netflix a constaté que les utilisateurs prenaient en moyenne 18 minutes pour choisir quoi regarder. Solution : "Trending Now", "Popular on Netflix" — réduire le champ de choix perçu.

**Progressive disclosure**
Montrer les options avancées uniquement quand l'utilisateur les demande explicitement.
```
[Options de base visibles]
+ Afficher les options avancées ↓
```

**Onboarding progressif**
Ne pas présenter toutes les fonctionnalités au premier lancement. Introduire les features au moment où l'utilisateur en a besoin.
Exemple Duolingo : déverrouiller les "Legendary Levels" uniquement après avoir complété un niveau normal.

**Recommandations**
Proposer une option par défaut ou recommandée réduit la charge de décision.
```
○ Mensuel — 9.99€/mois
● Annuel — 7.99€/mois  ← Recommandé (économisez 24%)
○ Lifetime — 199€
```

### Erreur fréquente
Afficher 12 options dans une dropdown alors que 4-5 couvrent 90% des cas. Ajouter "Autres options..." pour les cas rares.

---

## 5. Postel's Law (Robustness Principle)

> "Sois conservateur dans ce que tu fais, libéral dans ce que tu acceptes des autres."
>
> — Jon Postel (RFC 793, 1981)

### Principe
L'interface doit être robuste et s'adapter à l'utilisateur, pas l'inverse.

### Applications concrètes

**Inputs flexibles**
```
Téléphone accepté sous toutes les formes :
0612345678
06 12 34 56 78
+33 6 12 34 56 78
06-12-34-56-78
```

**Capitalisation flexible**
Les champs email doivent accepter `JOHN@EXAMPLE.COM` et `john@example.com` indifféremment.

**Responsive design**
S'adapter à toutes les tailles d'écran, résolutions et densités de pixels.

**Font size customization**
Amazon adapte sa navigation quand l'utilisateur augmente la taille de police du système : les liens de moindre importance disparaissent pour faire de la place.

**Input methods**
Accepter le clavier, la souris, le touch, et les technologies d'assistance (screen readers, switches).

### Erreur fréquente
Rejeter un numéro de téléphone parce qu'il contient des espaces ou des tirets. Le formatage est la responsabilité de l'interface, pas de l'utilisateur.

---

## 6. Peak-End Rule

> "Les gens jugent une expérience principalement par son pic émotionnel et sa fin, pas par la moyenne."
>
> — Kahneman & Fredrickson, 1993

### Principe
La mémorisation d'une expérience n'est pas la somme de tous ses moments. Elle est dominée par :
1. Le **moment le plus intense** (positif ou négatif)
2. La **fin** de l'expérience

### Applications concrètes

**Soigner la fin des flux**
- Confirmation de paiement → message chaleureux, résumé clair, prochaine étape évidente
- Inscription complétée → célébration visuelle, pas une page blanche
- Suppression d'un compte → message compréhensif, option de récupération

**Créer des pics positifs**
- Animation de succès après une action importante
- Message personnalisé après l'onboarding
- Easter egg ou micro-interaction surprise

**Atténuer les pics négatifs**
- Message d'erreur humain et actionnable (pas "Error 500")
- Page 404 utile avec des suggestions
- Loading state avec du contenu partiel (skeleton) plutôt qu'un spinner vide

**Duolingo**
Le "streak" (nombre de jours consécutifs) est un pic émotionnel fort. Perdre son streak est un pic négatif mémorisé longtemps — ce qui crée de l'engagement par aversion à la perte.

---

## 7. Aesthetic-Usability Effect

> "Les interfaces visuellement attractives sont perçues comme plus faciles à utiliser."
>
> — Kurosu & Kashimura, 1995 (Hitachi Design Center)

### Étude originale
26 layouts d'ATM testés avec 252 participants. Les designs visuellement attractifs étaient perçus comme plus faciles à utiliser, indépendamment de leur usabilité réelle.

### Implications
- Un beau design augmente la tolérance aux erreurs et aux bugs mineurs
- Un design attrayant génère plus de confiance initiale
- Les utilisateurs sont plus indulgents face aux problèmes si l'interface leur plaît

### Mise en garde
Cet effet peut masquer des problèmes d'usabilité réels. Les utilisateurs n'identifient pas toujours les problèmes d'un design attractif. Cela rend les tests utilisateurs d'autant plus importants.

---

## 8. Von Restorff Effect (Isolation Effect)

> "Parmi plusieurs objets similaires, celui qui diffère des autres est le plus susceptible d'être mémorisé."
>
> — Hedwig von Restorff, 1933

### Applications concrètes
- Badge "Nouveau" ou "Populaire" sur une option de pricing
- Bouton CTA d'une couleur qui rompt avec le reste de l'interface
- Élément mis en avant dans une liste (fond coloré, icône distinctive)

### Règle critique : ne pas sur-utiliser
Si tout est mis en valeur, rien ne l'est. Réserver la différenciation pour **1 ou 2 éléments maximum** par vue.

```
✗ Mauvais : 3 boutons colorés différemment + 2 badges "Nouveau"
✓ Bon : 1 bouton primaire clairement distinct + 1 badge "Recommandé"
```

---

## 9. Tesler's Law (Conservation of Complexity)

> "Pour tout système, il existe une certaine complexité qui ne peut pas être réduite."
>
> — Larry Tesler

### Principe
La complexité ne disparaît pas — elle se déplace. Si on simplifie l'interface, la complexité est transférée au développeur ou au système backend.

### Applications concrètes

**Bon exemple : formulaire d'adresse**
Option simple (utilisateur) : saisir l'adresse complète en texte libre
Option complexe (développeur) : parser, valider et normaliser l'adresse
→ Transférer la complexité au système (autocomplétion d'adresse) est le bon choix ici.

**Mauvais exemple : éditeur de code**
Masquer la syntaxe pour "simplifier" un éditeur de code transfère la complexité vers l'utilisateur qui ne comprend plus ce qui se passe.
→ Parfois la complexité doit rester visible à l'utilisateur.

### Paradoxe de l'utilisateur actif
Les utilisateurs commencent à utiliser un logiciel **immédiatement** sans lire la documentation. Ils préfèrent accomplir une tâche maintenant plutôt qu'apprendre le système d'abord. Concevoir en tenant compte de ce comportement.

---

## 10. Doherty Threshold

> "La productivité augmente considérablement quand système et utilisateur interagissent à moins de 400ms."
>
> — Walter Doherty & Ahrvind Thadani, 1982

### Seuils de perception
| Délai | Perception | Comportement |
|-------|-----------|-------------|
| < 100ms | Instantané | Sentiment de réactivité totale |
| 100–300ms | Quasi-instantané | Acceptable, pas de feedback nécessaire |
| 300–1000ms | Perceptible | Indicateur de chargement minimal recommandé |
| 1–10s | Attente | Progress bar ou skeleton nécessaire |
| > 10s | Abandon probable | Feedback détaillé + option d'annulation |

### Applications concrètes

**Optimistic UI**
Mettre à jour l'interface immédiatement (avant la réponse serveur) et rollback en cas d'erreur. L'utilisateur perçoit une réactivité totale.

**Skeleton screens**
Afficher la structure de la page (gris, forme des éléments) avant que le contenu charge. Réduit la perception de l'attente.

**Gmail loading animation**
Utiliser une animation de logo + barre de progression simple. Crée la perception d'un chargement plus court.

**Progress bars animées**
Les barres de progression qui s'animent légèrement semblent progresser plus vite. L'animation compense la perception de lenteur.

---

## Principes de Gestalt (fondement de l'organisation visuelle)

Bien qu'ils ne soient pas des "laws of UX" au sens strict, ils sous-tendent toutes les lois visuelles.

| Principe | Description | Usage UI |
|----------|-------------|---------|
| **Proximité** | Les éléments proches semblent liés | Grouper les éléments d'un formulaire |
| **Similarité** | Les éléments similaires semblent liés | Même style pour les items de même type |
| **Continuité** | L'œil suit une ligne ou une courbe | Alignements, rails de scroll horizontal |
| **Closure** | L'esprit complète les formes incomplètes | Icônes minimalistes, borders partielles |
| **Common Region** | Les éléments dans un conteneur semblent liés | Cards, groupes dans un formulaire |
| **Figure-Ground** | Distinguer l'objet principal de l'arrière-plan | Modales avec overlay, tooltips |

---

## Éthique et responsabilité

> "Avec ce pouvoir vient une responsabilité."

### Dark patterns à identifier et éviter

| Pattern | Description | Exemple |
|---------|-------------|---------|
| **Confirmshaming** | Intituler le refus de manière culpabilisante | "Non merci, je préfère payer plus cher" |
| **Hidden costs** | Révéler les frais uniquement à l'étape finale | Frais de service au checkout |
| **Roach motel** | Facile à entrer, difficile à sortir | Abonnement facile, résiliation laborieuse |
| **Misdirection** | Attirer l'attention loin de ce qui importe | Bouton désactivé vs option recommandée |
| **Disguised ads** | Publicités imitant du contenu | "Article sponsorisé" indiscernable |
| **Trick questions** | Formulaires avec pré-coches trompeuses | Newsletter cochée par défaut |

### La ligne entre persuasion et manipulation
- **Persuasion** : présenter la valeur réelle d'un produit, faciliter les bonnes décisions
- **Manipulation** : exploiter les biais cognitifs pour obtenir des actions que l'utilisateur regretterait

La règle : un design éthique améliore l'expérience de l'utilisateur **et** sert les objectifs du business. Pas l'un au détriment de l'autre.