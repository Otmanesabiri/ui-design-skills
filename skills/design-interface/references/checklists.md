# 08 - Checklists d'Execution UI

Sources : Laws of UX (Jakob, Hick, Fitts, Miller, Von Restorff, Doherty, Postel, Peak-End) - Refactoring UI - Practical UI

---

## Role du document

Ce fichier n'est pas une reference theorique. C'est la couche de controle avant production.

Objectif : transformer les principes UI en decisions verifiables, composant par composant.

Ordre d'application :
1. Respecter les conventions utilisateur
2. Reduire les choix visibles
3. Rendre les cibles faciles a atteindre
4. Structurer l'attention
5. Donner un feedback rapide et utile

Si deux regles se contredisent, privilegier l'utilisabilite, puis l'accessibilite, puis l'esthetique.

Deviation autorisee uniquement si le gain est mesurable : temps de tache reduit, taux d'erreur reduit, conversion amelioree, comprehension amelioree en test utilisateur. Sans preuve, revenir au pattern conventionnel.

---

## Les 4 forces fondamentales

Les lois UX sont regroupees en forces operationnelles. Ne pas les appliquer une par une au hasard.

| Force | Lois principales | Question de controle |
|---|---|---|
| Perception | Aesthetic-Usability, hierarchie visuelle, couleur | L'interface parait-elle claire avant meme d'etre lue ? |
| Attention | Von Restorff, Gestalt | L'oeil voit-il immediatement ce qui compte ? |
| Decision | Hick, Miller | Le choix principal est-il evident et limite ? |
| Interaction | Fitts, Doherty, Postel | L'action est-elle facile, rapide et tolerante ? |

### Priorite des lois

| Niveau | Loi | Statut |
|---|---|---|
| 1 | Jakob | Baseline obligatoire : utiliser les conventions connues |
| 1 | Hick | Limiter les choix visibles avant d'ajouter de la decoration |
| 1 | Fitts | Garantir des cibles atteignables et confortables |
| 2 | Miller | Grouper et decouper l'information dense |
| 2 | Von Restorff | Mettre en avant 1 element dominant, pas plus |
| 2 | Doherty | Repondre vite ou afficher un etat de progression |
| 3 | Postel | Accepter les formats utilisateur flexibles |
| 3 | Peak-End | Soigner les moments critiques et les fins de flux |
| 3 | Aesthetic-Usability | Renforcer la confiance par une execution visuelle propre |

---

## Contraintes non negociables

Ces contraintes s'appliquent par defaut a toute interface.

- 1 CTA primaire maximum par vue ou par decision active
- 5 choix visibles maximum sans structuration
- Choix illimites seulement s'ils sont groupes, filtres, hierarchises ou recherchables
- 44 x 44px minimum pour toute cible interactive tactile
- Feedback visible sous 300ms, sinon spinner, skeleton ou optimistic UI
- Aucun champ de formulaire sans label persistant
- Aucune erreur sans cause comprehensible et solution concrete
- Aucun bouton icon-only sans nom accessible et tooltip si le sens n'est pas universel
- Aucun pattern non conventionnel pour navigation, fermeture, recherche, retour ou soumission
- Aucun element mis en evidence si son action n'est pas prioritaire
- Aucun etat vide sans explication et prochaine action utile
- Hierarchie validee en grayscale avant ajout de couleur
- Contraste AA minimum sur texte et controles fonctionnels
- Focus visible et navigation clavier complete

---

## Checklist globale de vue

Avant de valider une page ou un ecran :

- L'action principale est identifiable en moins de 3 secondes
- Les actions secondaires sont visuellement moins fortes que l'action principale
- Les informations sont groupees par proximite et similarite
- Les sections non liees sont separees par plus d'espace que les elements lies
- Les choix visibles sont limites aux options utiles maintenant
- Les options rares ou avancees sont cachees derriere une divulgation progressive
- Les conventions de navigation et d'interaction sont respectees
- Les textes importants restent lisibles en contraste, taille et longueur
- 3 niveaux de hierarchie maximum sont visibles simultanement dans une zone
- La lecture rapide suit un parcours F ou Z selon le type de page
- Les lignes de texte courant restent a 80 caracteres maximum
- Les etats loading, empty, error, success et disabled existent
- Le parcours se termine par une confirmation claire ou une prochaine etape evidente

---

## Controle de flux

Une interface ne se valide pas seulement ecran par ecran. Le parcours complet doit rester coherent.

Checklist :
- Le debut du flux indique clairement l'objectif et les pre-requis
- Chaque transition explique ce qui vient de changer
- Les donnees saisies ou selectionnees sont conservees entre les etapes
- Les retours en arriere ne punissent pas l'utilisateur
- La fin confirme le resultat obtenu
- La prochaine action utile est evidente apres la fin du flux
- Les moments critiques ont un feedback plus soigne que les actions ordinaires

---

## Mapping par composant

### Boutons

Lois dominantes : Fitts, Von Restorff, Hick.

Regles :
- Taille interactive minimale : 44 x 44px
- 1 bouton primaire maximum dans un groupe d'actions
- Pas de double CTA equivalent
- Texte = verbe d'action precis, pas "OK" ou "Submit"
- Action dangereuse visuellement separee de l'action courante
- Actions frequentes dans la zone du pouce sur mobile
- Actions critiques isolees spatialement des actions ordinaires
- Bords et coins utilises pour les actions persistantes ou frequentes quand le contexte s'y prete
- Focus, hover, active, disabled et loading obligatoires

Checklist :
- Le bouton primaire est-il le seul element dominant ?
- Les boutons secondaires ressemblent-ils vraiment a des options secondaires ?
- Le bouton est-il atteignable confortablement sur mobile ?
- Sa position reduit-elle aussi la distance d'action, pas seulement sa taille ?
- Le libelle annonce-t-il le resultat de l'action ?

### Formulaires

Lois dominantes : Miller, Hick, Postel.

Regles :
- Label persistant obligatoire pour chaque champ
- Grouper les champs par theme
- Decouper en multi-step si le formulaire depasse 5 a 7 champs visibles
- Validation au blur, sauf feedback positif non intrusif
- Accepter les formats courants de saisie : espaces, tirets, casse, prefixes
- Normaliser la saisie cote systeme, pas cote utilisateur
- Afficher ensuite une valeur canonique claire
- Message d'erreur = probleme + cause si utile + correction

Checklist :
- Peut-on comprendre le champ sans placeholder ?
- Les champs lies sont-ils proches les uns des autres ?
- Les champs optionnels sont-ils evites ou reveles progressivement ?
- L'utilisateur peut-il revenir en arriere sans perdre ses donnees ?
- Un format humain courant est-il accepte meme s'il differe du format stocke ?
- Chaque erreur dit-elle comment la resoudre ?

### Navigation

Lois dominantes : Jakob, Hick, Gestalt.

Regles :
- Utiliser les conventions : top nav, sidebar, tabs, breadcrumbs selon le contexte
- Limiter les entrees visibles au premier niveau
- Grouper les items par usage, pas par structure interne de l'entreprise
- Signaler clairement l'emplacement actuel
- Garder les actions globales et locales separees

Checklist :
- Un utilisateur peut-il predire ou se trouve une fonction standard ?
- Les items de navigation sont-ils organises en groupes evidents ?
- Le niveau actif est-il visible sans dependance a la couleur seule ?
- Les destinations rares sont-elles deplacees dans "Plus", settings ou recherche ?

### Dashboard

Lois dominantes : Hierarchie, Miller, Gestalt, Hick.

Regles :
- Mettre les indicateurs decisionnels avant les donnees decoratives
- Limiter les KPIs principaux a 3-5
- Grouper les donnees par decision a prendre ; les donnees peuvent etre nombreuses si elles restent filtrees, scannables et hierarchisees
- Aligner les nombres a droite, les labels a gauche
- Eviter les cartes repetitives si une table ou une liste scannable est plus efficace
- Autoriser un niveau 2 de hierarchie pour les signaux secondaires, sans concurrencer le signal principal de chaque zone

Checklist :
- La question principale du dashboard est-elle evidente ?
- Les donnees importantes dominent-elles les donnees secondaires ?
- Chaque visualisation supporte-t-elle une decision concrete ?
- Les filtres visibles sont-ils les plus utilises ?
- Les vues expertes gardent-elles une structure de scan claire malgre la densite ?

### Feedback et etats

Lois dominantes : Doherty, Peak-End, Aesthetic-Usability.

Regles :
- Sous 300ms : pas forcement de feedback visuel
- 300ms a 1s : spinner discret ou etat pending local
- 1s a 3s : skeleton ou structure de contenu
- Plus de 3s : progression, texte d'etat ou possibilite d'annuler
- Prefetch, cache ou pre-rendu pour les actions frequentes et previsibles
- Optimistic UI par defaut pour les actions non critiques et reversibles
- Succes : confirmer l'action et montrer la prochaine etape
- Erreur : expliquer sans jargon et proposer une action

Checklist :
- L'utilisateur sait-il que son action a ete prise en compte ?
- Le chargement preserve-t-il la structure attendue ?
- Le systeme peut-il eviter l'attente plutot que seulement l'habiller ?
- La fin du flux laisse-t-elle une impression claire et rassurante ?
- Les erreurs sont-elles actionnables ?

### Modales et dialogs

Lois dominantes : Hick, Jakob, Fitts.

Regles :
- Une modale = une decision
- Bouton de fermeture visible en haut a droite
- Echap et clic overlay selon le niveau de risque
- Focus trap obligatoire
- Actions en bas, primaire clairement distinguee
- Action destructive confirmee par un texte explicite

Checklist :
- La modale demande-t-elle une seule chose ?
- Peut-on la fermer de maniere conventionnelle ?
- L'action dangereuse est-elle impossible a declencher par accident ?
- Le focus clavier reste-t-il dans la modale ?

---

## Consolidation des lois redondantes

Ne pas empiler les principes quand ils disent la meme chose.

| Phenomenes | Lois associees | Regle unique |
|---|---|---|
| Charge cognitive | Hick + Miller | Limiter les choix non structures ; grouper, filtrer ou rechercher le reste |
| Attention | Von Restorff + hierarchie visuelle | 1 element dominant par zone de decision, avec niveau 2 autorise |
| Organisation | Gestalt + espacement | Proximite = relation, distance = separation |
| Confiance percue | Aesthetic-Usability + couleur + typographie | Execution propre, contraste lisible, rythme stable |
| Rapidite percue | Doherty + feedback | Eviter l'attente par cache/prefetch/optimistic UI ; sinon montrer l'etat du systeme |

---

## Liens avec les autres fichiers

Le systeme doit etre imbrique, pas parallele.

| Fichier | Role dans le systeme | Lois executees |
|---|---|---|
| `hierarchie-visuelle.md` | Prioriser ce qui doit etre vu | Von Restorff, Aesthetic-Usability |
| `espacement-layout.md` | Grouper, separer, guider l'oeil | Gestalt, Miller |
| `couleur-systeme.md` | Signaler statut, importance, accessibilite | Hierarchie, Aesthetic-Usability |
| `composants.md` | Transformer les principes en elements reutilisables | Fitts, Hick, Postel, Doherty |
| `lois-ux.md` | Reference theorique | Toutes, sans arbitrage de production |

Regle d'usage :
- Lire `lois-ux.md` pour comprendre
- Utiliser ce fichier pour decider
- Verifier `composants.md` pour implementer

---

## Audit rapide avant livraison

Bloquant :
- Plus d'un CTA primaire dans la meme decision
- Cible interactive sous 44 x 44px sur touch
- Champ sans label
- Erreur sans solution
- Navigation non conventionnelle sans justification forte
- Loading de plus de 1s sans feedback
- Contraste sous AA sur texte ou controle fonctionnel
- Focus visible absent
- Navigation clavier incomplete
- Hierarchie illisible en grayscale

Majeur :
- Plus de 5 choix visibles sans groupement, filtre, recherche ou hierarchie claire
- Plusieurs elements visuellement dominants
- Options avancees visibles par defaut
- Contraste faible sur texte fonctionnel
- Etats hover/focus/disabled/loading manquants
- Flux sans debut clair, transition explicite ou fin exploitable
- Interface dense sans parcours de scan clair

Mineur :
- Microcopy vague
- Espacement incoherent entre groupes
- Fin de flux plate ou peu informative
- Animation decorative sans fonction
- Lignes de texte courant trop longues

Decision :
- Tout bloquant doit etre corrige avant livraison
- Les majeurs doivent etre corriges ou explicitement acceptes
- Les mineurs peuvent entrer dans une passe de polish
