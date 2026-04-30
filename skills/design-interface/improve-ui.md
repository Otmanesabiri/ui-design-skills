# Improve UI - Procedure d'amelioration

Objectif : ameliorer une interface existante sans la reinventer inutilement. Priorite aux problemes qui bloquent la comprehension, l'action, l'accessibilite ou la confiance.

References a mobiliser :
- `references/checklists.md` pour classer les problemes
- `references/hierarchie-visuelle.md` pour corriger la priorisation
- `references/espacement-layout.md` pour clarifier les groupes
- `references/couleur-systeme.md` pour contraste et signaux
- `references/composants.md` pour etats et patterns
- `references/antipatterns-ethique.md` pour eviter les manipulations

---

## 1. Diagnostiquer avant de modifier

Lire l'interface comme un utilisateur presse.

Questions :
- Que dois-je faire ici ?
- Quelle action est la plus importante ?
- Qu'est-ce qui est secondaire ?
- Ou puis-je me tromper ?
- Qu'est-ce qui semble cliquable mais ne l'est pas ?
- Qu'est-ce qui est cliquable mais ne se voit pas ?

Classer les problemes :
- Bloquant : empeche l'usage, l'accessibilite ou la decision
- Majeur : ralentit, confond ou augmente le risque d'erreur
- Mineur : polish, coherence, confort

---

## 2. Ordre de correction

Ne pas commencer par la couleur.

1. Clarifier l'objectif de la vue
2. Reduire ou structurer les choix
3. Reparer la hierarchie visuelle
4. Corriger l'espacement et les groupes
5. Corriger les composants et leurs etats
6. Corriger accessibilite et clavier
7. Ajouter le polish visuel

Regle : si une correction est seulement esthetique mais ne resout aucun probleme de comprehension ou d'usage, la repousser.

---

## 3. Corrections frequentes

### Trop de bruit visuel

Symptomes :
- Plusieurs boutons semblent primaires
- Trop de badges, couleurs ou shadows
- Les titres, cartes et actions ont le meme poids

Corrections :
- Garder 1 element dominant par zone de decision
- De-emphasiser les actions secondaires
- Reduire les shadows et fonds decoratifs
- Tester la page en grayscale

### Trop de choix

Symptomes :
- Longues listes d'actions visibles
- Filtres et options avancees toujours ouverts
- L'utilisateur doit lire avant de savoir quoi faire

Corrections :
- Garder 3-5 choix non structures visibles
- Grouper, filtrer ou rechercher les choix nombreux
- Mettre les options rares derriere "Plus" ou "Avance"
- Proposer une option recommandee si utile

### Formulaire dur a remplir

Symptomes :
- Placeholders utilises comme labels
- Erreurs tardives ou vagues
- Format impose trop strict
- Champs optionnels partout

Corrections :
- Labels persistants
- Groupement par theme
- Validation au blur
- Formats flexibles puis affichage canonique
- Erreur = probleme + solution
- Champs optionnels reveles progressivement

### Dashboard lourd

Symptomes :
- Trop de cards identiques
- KPIs sans decision associee
- Table illisible
- Filtres trop nombreux

Corrections :
- Limiter les KPIs principaux a 3-5
- Transformer les cards repetitives en table ou liste
- Aligner nombres a droite
- Ajouter tri, filtre, recherche si volume important
- Garder un parcours de scan clair

### Feedback faible

Symptomes :
- Rien ne se passe apres clic
- Loading global pour une action locale
- Erreur technique brute
- Succes sans prochaine etape

Corrections :
- Feedback local sous 300ms
- Optimistic UI pour actions reversibles
- Skeleton pour contenu structure
- Messages humains et actionnables
- Fin de flux avec resultat + prochaine action

---

## 4. Regles d'intervention

Faire :
- Conserver les patterns existants quand ils fonctionnent
- Corriger par petites passes verifiables
- Utiliser les tokens existants avant d'en creer
- Renforcer la hierarchie par taille, poids, espacement et contraste
- Verifier mobile et desktop

Eviter :
- Ajouter une nouvelle palette pour masquer un probleme de structure
- Remplacer toutes les cards par d'autres cards
- Ajouter une animation sans fonction
- Utiliser la couleur seule pour signaler un etat
- Casser une convention sans gain mesurable

---

## 5. Checklist avant/apres

Avant de finir :
- Le probleme initial est-il resolu ?
- L'action principale est-elle plus evidente ?
- Le nombre de choix non structures a-t-il baisse ?
- Les zones liees sont-elles mieux groupees ?
- Les contrastes et focus sont-ils conformes ?
- Les etats loading, error, empty, success existent-ils ?
- La densite reste-t-elle scannable ?
- Aucun dark pattern n'a ete introduit ?

Livrable attendu :
- Liste courte des changements
- Pourquoi chaque changement ameliore l'usage
- Risques restants ou points a tester
