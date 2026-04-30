# Generate UI - Procedure de creation

Objectif : produire une interface utilisable des le premier ecran, coherente avec les references du skill, sans commencer par une page marketing ou une decoration gratuite.

References a mobiliser :
- `references/processus-decisions.md` pour cadrer la feature
- `references/checklists.md` pour les contraintes executables
- `references/hierarchie-visuelle.md` pour prioriser les contenus
- `references/espacement-layout.md` pour organiser la page
- `references/couleur-systeme.md` et `references/tokens.md` pour les valeurs visuelles
- `references/composants.md` pour les composants attendus
- `references/antipatterns-ethique.md` pour les garde-fous

---

## 1. Cadrer avant de dessiner

Ne pas commencer par "faire une belle page". Commencer par la tache utilisateur.

Questions obligatoires :
- Qui utilise cette interface ?
- Quelle action principale doit etre accomplie ?
- Quelle information est necessaire avant cette action ?
- Quelle information peut etre cachee, differee ou calculee ?
- Quel est le risque principal : confusion, erreur, lenteur, manque de confiance ?

Sortie attendue :
- 1 objectif principal
- 1 CTA primaire
- 3 a 5 informations ou actions visibles en priorite
- Les etats necessaires : loading, empty, error, success, disabled

---

## 2. Construire la structure

Ordre de construction :
1. Contenu et donnees
2. Hierarchie
3. Layout
4. Composants
5. Couleur
6. Micro-interactions

Regles :
- Designer d'abord en grayscale mentalement : la couleur ne doit pas porter seule la hierarchie
- 1 element dominant par zone de decision
- 3 niveaux de hierarchie visibles maximum dans une zone
- Les elements lies sont proches ; les groupes distincts sont clairement separes
- Les lignes de texte courant restent a 80 caracteres maximum

---

## 3. Choisir le layout selon le produit

### SaaS, CRM, admin, dashboard

Priorite : densite lisible, scan rapide, actions previsibles.

Patterns recommandes :
- Sidebar ou top nav conventionnelle
- Header compact avec titre, contexte et actions
- Tables ou listes scannables pour donnees repetitives
- Filtres visibles seulement s'ils sont frequents
- Panels, drawers ou pages detail pour complexite secondaire

Eviter :
- Hero marketing
- Grandes cards decoratives pour donnees tabulaires
- Illustrations qui remplacent les controles utiles
- Couleur utilisee comme seul signal

### App grand public

Priorite : parcours simple, decision claire, feedback rassurant.

Patterns recommandes :
- Navigation familiere
- CTA primaire visible
- Divulgation progressive
- Empty states utiles
- Confirmation claire en fin de flux

### Landing page ou page de marque

Priorite : comprehension immediate de l'offre.

Patterns recommandes :
- Le produit, lieu, service ou objet doit etre visible des le premier viewport
- H1 = nom, offre ou categorie concrete
- Image reelle ou scene visuelle pertinente
- Un hint de la section suivante reste visible
- CTA principal unique

---

## 4. Appliquer les contraintes non negociables

Avant d'implementer :
- 1 CTA primaire maximum par decision active
- 5 choix visibles maximum sans structuration
- Choix nombreux autorises si groupes, filtres, hierarchises ou recherchables
- 44 x 44px minimum pour cible touch
- Feedback sous 300ms ou etat de progression
- Aucun champ sans label persistant
- Aucune erreur sans solution
- Focus visible et navigation clavier complete
- Contraste AA minimum sur texte et controles fonctionnels
- Hierarchie lisible en grayscale

---

## 5. Composer les composants

### Boutons

- Texte avec verbe d'action precis
- Primaire = action principale seulement
- Secondaire = alternative utile mais moins importante
- Tertiaire = action annexe, lien ou texte discret
- Actions dangereuses separees spatialement
- Loading state conserve la largeur du bouton si possible

### Formulaires

- Labels persistants au-dessus des champs
- Champs groupes par theme
- Multi-step si le formulaire devient dense
- Validation au blur
- Formats flexibles acceptes puis normalises
- Erreurs actionnables sous le champ concerne

### Navigation

- Respecter les conventions du type de produit
- Item actif visible sans dependance a la couleur seule
- Regrouper par usage utilisateur
- Mettre les destinations rares dans recherche, settings ou "Plus"

### Dashboard

- KPIs principaux limites a 3-5
- Donnees nombreuses autorisees si scannables
- Filtres utiles en haut ou pres des donnees concernees
- Nombres alignes a droite
- Statuts accompagnes de texte ou icone, pas couleur seule

---

## 6. Gerer les etats

Chaque interface generee doit prevoir :

| Etat | Exigence |
|---|---|
| Loading | Spinner local, skeleton ou optimistic UI selon duree |
| Empty | Message utile + prochaine action |
| Error | Cause claire + solution |
| Success | Confirmation + prochaine etape |
| Disabled | Raison explicite si l'action semble attendue |
| Focus | Indicateur visible au clavier |

Regle Doherty :
- Eviter l'attente avec cache, prefetch, pre-rendu ou optimistic UI
- Si l'attente reste visible, montrer l'etat du systeme

---

## 7. Verifier avant livraison

Checklist finale :
- L'objectif de l'ecran est clair en moins de 3 secondes
- Le CTA primaire est unique
- Les choix nombreux sont structures
- La hierarchie fonctionne sans couleur
- Les tailles touch respectent 44 x 44px
- Les transitions de flux sont explicites
- Les erreurs ne culpabilisent pas l'utilisateur
- Le design n'utilise aucun dark pattern
- L'interface reste lisible sur mobile et desktop
- Aucun texte ne deborde de son conteneur

Resultat attendu : une UI fonctionnelle, scannable, accessible et directement exploitable.
