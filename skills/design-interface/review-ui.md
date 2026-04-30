# Review UI - Procedure d'audit

Objectif : evaluer une interface avec une posture de review. Les problemes passent avant les compliments. Les constats doivent etre actionnables, classes par severite, et relies a un impact utilisateur.

References a mobiliser :
- `references/checklists.md` pour les blocants et majeurs
- `references/lois-ux.md` pour expliquer le principe si necessaire
- `references/composants.md` pour verifier les patterns
- `references/couleur-systeme.md` pour accessibilite couleur
- `references/antipatterns-ethique.md` pour risques de manipulation

---

## Format de sortie recommande

1. Findings critiques et majeurs
2. Questions ouvertes ou hypotheses
3. Points positifs utiles
4. Synthese courte

Chaque finding doit contenir :
- Severite : bloquant, majeur, mineur
- Localisation : ecran, zone, composant ou fichier si disponible
- Probleme observe
- Impact utilisateur
- Correction recommandee

Eviter les avis vagues : "c'est joli", "c'est moderne", "a ameliorer".

---

## Grille de severite

### Bloquant

Probleme qui empeche ou compromet fortement l'usage :
- CTA principal absent ou concurrence par un autre CTA primaire
- Champ sans label
- Erreur sans solution
- Contraste sous AA sur texte fonctionnel
- Focus visible absent
- Navigation clavier incomplete
- Cible tactile sous 44 x 44px
- Action dangereuse trop facile a declencher
- Dark pattern manifeste

### Majeur

Probleme qui ralentit, confond ou augmente les erreurs :
- Plus de 5 choix visibles sans structuration
- Hierarchie illisible en grayscale
- Trop d'elements dominants dans une zone
- Options avancees visibles par defaut
- Loading long sans structure de feedback
- Flux sans debut clair, transition explicite ou fin utile
- Dashboard dense sans scan possible
- Couleur utilisee comme seul signal

### Mineur

Probleme de polish ou de coherence :
- Microcopy vague
- Espacement incoherent
- Lignes de texte trop longues
- Animation sans fonction
- Arrondis, shadows ou paddings incoherents
- Etat vide peu engageant mais non bloquant

---

## Checklist d'audit

### Objectif et decision

- L'objectif de la vue est-il clair en moins de 3 secondes ?
- L'action principale est-elle unique ?
- Les actions secondaires sont-elles visuellement secondaires ?
- Les choix nombreux sont-ils groupes, filtres, hierarchises ou recherchables ?
- Existe-t-il une option recommandee quand le choix est complexe ?

### Hierarchie et scan

- La page fonctionne-t-elle en grayscale ?
- 3 niveaux de hierarchie maximum sont-ils visibles dans une zone ?
- La lecture suit-elle un parcours F ou Z coherent ?
- Les titres, labels, valeurs et actions ont-ils des poids distincts ?
- Les donnees importantes dominent-elles les donnees decoratives ?

### Layout et espacement

- Les elements lies sont-ils proches ?
- Les groupes distincts ont-ils assez d'espace ?
- Les alignements facilitent-ils la comparaison ?
- Les cards sont-elles utiles ou remplacent-elles une table plus efficace ?
- La densite est-elle adaptee au type de produit ?

### Composants

- Boutons : tailles, etats, libelles et hierarchie corrects ?
- Formulaires : labels persistants, validation au blur, erreurs actionnables ?
- Navigation : conventionnelle, groupee, active state clair ?
- Tables : alignement, tri, statut, actions et empty state corrects ?
- Modales : une decision, fermeture claire, focus trap ?

### Feedback et flux

- L'interface repond-elle sous 300ms ou explique-t-elle l'attente ?
- Cache, prefetch ou optimistic UI sont-ils possibles ?
- Les transitions de flux sont-elles explicites ?
- La fin du parcours confirme-t-elle le resultat ?
- La prochaine action est-elle evidente ?

### Accessibilite

- Contraste AA minimum ?
- Focus visible ?
- Navigation clavier complete ?
- Labels et noms accessibles ?
- Couleur doublee par texte, icone ou forme ?
- Texte lisible et non tronque ?

### Ethique

- L'utilisateur peut-il refuser aussi facilement qu'accepter ?
- Les couts, consequences et engagements sont-ils visibles avant action ?
- Les options sont-elles formulees sans culpabilisation ?
- Les defaults servent-ils l'utilisateur autant que le business ?
- La sortie d'un abonnement, compte ou flux est-elle accessible ?

---

## Red flags immediats

Arreter la review et signaler fortement si :
- Bouton primaire utilise pour une action trompeuse
- Refus masque, affaibli ou culpabilisant
- Frais reveles tardivement
- Desabonnement plus difficile que l'inscription
- Consentement pre-coche
- Donnees destructives sans confirmation claire
- Interface inutilisable au clavier

---

## Exemple de finding

Bloquant - Formulaire de paiement

Le champ "Code postal" n'a pas de label persistant et utilise seulement un placeholder. Des que l'utilisateur saisit une valeur, le sens du champ disparait, ce qui augmente le risque d'erreur et pose un probleme d'accessibilite. Ajouter un label visible au-dessus du champ et conserver le placeholder uniquement comme exemple de format.

---

## Decision finale

Utiliser cette conclusion :
- Pret : aucun bloquant, majeurs acceptes ou corriges
- Pret avec reserves : aucun bloquant, quelques majeurs documentes
- Non pret : au moins un bloquant ou risque ethique majeur
