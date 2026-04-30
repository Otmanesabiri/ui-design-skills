# 01 — Processus & Décisions Design

Sources : Refactoring UI ch.1 · Practical UI ch.1 (Fundamentals)

---

## Par où commencer

### Règle fondamentale : feature d'abord, layout ensuite
Ne jamais commencer par "design l'app". Commencer par une feature concrète et fonctionnelle.

**Mauvaise approche :**
- Où va la navigation ?
- Top nav ou sidebar ?
- Où place-t-on le logo ?

Ces questions sont prématurées. Sans avoir designé quelques features, tu n'as pas les informations pour y répondre.

**Bonne approche :**
Choisir la première feature à designer (ex : "rechercher un vol") et lister uniquement ce dont elle a besoin :
- Champ ville de départ
- Champ ville d'arrivée
- Champ date aller
- Champ date retour
- Bouton de recherche

Commencer par ça. Le layout émerge naturellement après.

---

## Travailler en basse fidélité

### Pourquoi
Dans les premières étapes, s'attarder sur les polices, les ombres et les couleurs est une perte de temps. Ces décisions dépendent du contenu et de la structure — qui ne sont pas encore définies.

### Comment
- Dessiner sur papier avec un Sharpie épais — impossible de s'attarder sur les détails
- Designer en grayscale dans l'outil de design — force l'usage de l'espacement, du contraste et de la taille comme seuls leviers de hiérarchie
- Les wireframes sont **jetables** — ne pas sur-investir dedans

### Bénéfice du grayscale
En grayscale, tu es forcé d'utiliser :
- L'espacement pour créer de la séparation
- Le contraste pour créer de l'importance
- La taille pour signaler la hiérarchie

Résultat : une interface avec une hiérarchie forte et claire, facile à enrichir avec de la couleur par la suite.

---

## Ne pas over-designer

### Ne pas prévoir des features hypothétiques
Designer uniquement ce dont les utilisateurs ont besoin aujourd'hui. Les features hypothétiques ("et si l'utilisateur veut faire X ?") alourdissent l'interface sans valeur prouvée.

### Itérer rapidement
Les maquettes statiques n'ont pas de valeur pour les utilisateurs. Les utiliser pour explorer des idées, puis les laisser derrière dès qu'une direction est validée. Passer à l'implémentation réelle le plus vite possible.

---

## Choisir une personnalité

Avant de choisir les couleurs et les polices, définir la personnalité de l'interface. La personnalité dicte les choix esthétiques.

### Axes de personnalité

| Personnalité | Typographie | Couleur | Border-radius |
|---|---|---|---|
| Élégant / classique | Serif | Or, noir, blanc | Petit (2-4px) |
| Neutre / professionnel | Sans-serif neutre | Bleu, gris | Moyen (4-8px) |
| Ludique / accessible | Sans-serif arrondi | Couleurs vives | Grand (8-16px+) |
| Sécurisant / institutionnel | Sans-serif lisible | Bleu, vert | Moyen |

### Couleur et psychologie
- **Bleu** : sûr, familier, universel — personne ne se plaint du bleu
- **Or / Jaune foncé** : premium, sophistiqué, luxe
- **Rose** : léger, décontracté, pas sérieux
- **Vert** : nature, santé, succès, croissance
- **Rouge** : danger, urgence, énergie
- **Violet** : créativité, spiritualité, mystère

---

## Limiter les choix

### Le problème de la liberté totale
Quand on a trop d'options, on perd du temps à décider. La solution est de définir des systèmes à l'avance qui contraignent les choix à un ensemble raisonnable.

### Systèmes à définir en amont
1. **Palette de couleurs** — 8-10 nuances par couleur, définies une fois
2. **Échelle typographique** — 8-10 tailles fixes
3. **Système d'espacement** — valeurs prédéfinies (4/8/16/24/32…)
4. **Échelle de shadows** — 5 niveaux d'élévation
5. **Border-radius** — 2-3 valeurs fixes

Une fois ces systèmes définis, chaque décision se résume à "quelle valeur du système utiliser ?" plutôt que "quelle valeur inventer ?".

---

## Avoir une raison logique pour chaque détail

### Principe fondamental (Practical UI)
L'importance du design UI est souvent réduite à "faire joli". C'est une erreur. Si une interface est bien designée, **chaque détail a une raison logique qui améliore l'utilisabilité**.

Certains éléments sont purement décoratifs, mais même eux doivent avoir une justification : créer de la profondeur, guider l'œil, signaler une hiérarchie.

### Question à se poser pour chaque élément
> "Pourquoi cet élément est là ? Qu'est-ce qu'il communique ou améliore ?"

Si la réponse est "parce que c'est joli", envisager de le supprimer.

---

## Framework de décision quand deux options s'affrontent

Évaluer dans cet ordre strict :

1. **Utilisabilité** — Laquelle réduit le plus le risque de confusion ou d'erreur ?
2. **Hiérarchie** — Laquelle communique mieux l'importance relative ?
3. **Accessibilité** — Laquelle est utilisable par le plus grand nombre ?
4. **Cohérence** — Laquelle respecte les patterns déjà établis dans l'interface ?
5. **Esthétique** — Laquelle est la plus belle, à critères égaux sur les 4 points précédents ?

L'esthétique est le **dernier critère**, pas le premier.

---

## Minimiser les risques d'utilisabilité (Practical UI)

Baser les décisions de design sur le risque : **quelle est la probabilité qu'un utilisateur ait du mal avec cet élément ?**

### Risques fréquents à identifier avant de finir un design
- Texte gris clair sur fond blanc → risque de lisibilité pour les malvoyants
- Icône sans label → risque de non-compréhension (surtout pour les troubles cognitifs)
- Texte de titre en couleur → risque de confusion avec un lien
- Champs de formulaire sans bordure visible → risque de non-identification comme champ interactif
- Bouton sans état focus visible → risque d'inaccessibilité clavier

### Process recommandé
Avant tout test utilisateur, identifier et corriger les risques évidents. Le test utilisateur sert à révéler les risques subtils, pas les risques grossiers qui peuvent être résolus par le bon sens.