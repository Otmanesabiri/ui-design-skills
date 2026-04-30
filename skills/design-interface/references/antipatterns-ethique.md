# Antipatterns & Ethique UI

Objectif : identifier et eviter les interfaces qui exploitent les biais cognitifs contre l'interet de l'utilisateur. Une interface persuasive peut guider. Une interface manipulatrice pousse l'utilisateur vers une action qu'il pourrait regretter.

Principe :
- Persuasion acceptable : clarifie la valeur, reduit la friction, aide a decider
- Manipulation interdite : cache, deforme, culpabilise, piege ou rend le refus difficile

---

## Regle de base

Une decision utilisateur doit etre :
- Informee : consequences, couts et conditions visibles avant l'action
- Libre : accepter et refuser sont tous deux accessibles
- Reversible quand le risque est eleve
- Comprehensible sans jargon
- Non dependante d'une pression artificielle

Si le design fonctionne seulement parce que l'utilisateur ne voit pas, ne comprend pas ou n'ose pas refuser, c'est un dark pattern.

---

## Antipatterns critiques

### Confirmshaming

Definition : formuler le refus de maniere culpabilisante ou humiliante.

Exemples :
- "Non merci, je prefere payer plus cher"
- "Je ne veux pas progresser"
- "Ignorer cette opportunite"

Correction :
- Utiliser un refus neutre : "Non merci", "Continuer sans abonnement", "Plus tard"

### Hidden costs

Definition : reveler les frais, taxes, conditions ou engagements seulement en fin de parcours.

Correction :
- Afficher le cout total avant l'action engageante
- Expliquer les frais variables des qu'ils deviennent calculables
- Ne pas utiliser le checkout comme moment de surprise

### Roach motel

Definition : entrer est simple, sortir est difficile.

Cas typiques :
- Inscription en 1 clic, desabonnement en support manuel
- Suppression de compte cachee
- Annulation derriere plusieurs confirmations asymetriques

Correction :
- Sortie aussi accessible que l'entree
- Annulation dans les settings attendus
- Confirmation claire, sans friction punitive

### Misdirection

Definition : attirer l'attention vers une action benefique au business et loin de l'action importante pour l'utilisateur.

Correction :
- Hierarchie fondee sur l'importance utilisateur
- Actions destructives ou engageantes visibles et explicites
- Pas de couleur primaire pour masquer une option moins favorable

### Disguised ads

Definition : publicite ou contenu sponsorise presente comme contenu normal.

Correction :
- Label "Sponsorise", "Publicite" ou equivalent visible
- Style distinct du contenu editorial ou fonctionnel
- Pas d'imitation de notification systeme

### Trick questions

Definition : formulation ambigue, double negation ou checkbox qui inverse l'intention.

Exemples :
- "Decochez cette case si vous ne souhaitez pas ne pas recevoir..."
- Consentement pre-coche

Correction :
- Phrase positive simple
- Consentement opt-in explicite
- Une case = une intention claire

### Forced continuity

Definition : convertir un essai gratuit en paiement sans rappel clair.

Correction :
- Rappel avant facturation
- Date et montant visibles
- Annulation simple avant renouvellement

### Sneaking

Definition : ajouter un produit, service, assurance ou option sans action explicite.

Correction :
- Options additionnelles en opt-in
- Resume clair avant paiement
- Aucun ajout automatique au panier

### Scarcity ou urgency artificielle

Definition : fausse rarete ou faux compte a rebours pour accelerer la decision.

Correction :
- Utiliser l'urgence seulement si elle est reelle et verifiable
- Expliquer la cause : stock, date limite, capacite
- Ne pas reinitialiser un timer artificiellement

### Obstruction

Definition : rendre une action utile inutilement longue ou confuse.

Cas typiques :
- Fermer un compte
- Exporter ses donnees
- Refuser le tracking
- Modifier un abonnement

Correction :
- Chemin direct
- Libelles explicites
- Pas d'etapes inutiles

---

## Patterns sensibles

Ces patterns ne sont pas interdits, mais doivent etre controles.

### Defaults

Acceptable si :
- Le choix par defaut correspond a l'interet probable de l'utilisateur
- Il est visible
- Il est facile a changer

Risque si :
- Option payante cochee par defaut
- Consentement donne par inaction
- Choix recommande sans justification

### Recommandations

Acceptable si :
- La recommandation est expliquee
- Les alternatives restent comparables
- Les criteres sont utiles a l'utilisateur

Risque si :
- "Recommande" signifie seulement "plus rentable"
- L'option mise en avant cache un engagement

### Gamification

Acceptable si :
- Elle motive sans punir
- Elle laisse le controle a l'utilisateur
- Elle ne cree pas d'anxiete excessive

Risque si :
- Streaks, pertes ou recompenses poussent a des comportements regrettables
- Notifications culpabilisantes

### Personnalisation

Acceptable si :
- Les donnees utilisees sont pertinentes
- Le controle est explicite
- L'utilisateur peut modifier ou desactiver

Risque si :
- Profilage opaque
- Prix ou options manipules selon vulnerabilite supposee

---

## Checklist ethique avant livraison

- L'utilisateur comprend-il ce qu'il accepte ?
- Peut-il refuser sans humiliation ni friction excessive ?
- Le cout total est-il visible avant engagement ?
- Les consequences importantes sont-elles explicites ?
- Le consentement est-il opt-in quand il concerne donnees, marketing ou paiement ?
- L'annulation est-elle aussi trouvable que l'inscription ?
- Les actions destructives demandent-elles confirmation ?
- Les messages d'erreur aident-ils au lieu de blamer ?
- Les options recommandees sont-elles justifiables cote utilisateur ?
- Le design reste-t-il acceptable si l'utilisateur est fatigue, presse ou novice ?

---

## Red flags bloquants

- Consentement pre-coche pour tracking, marketing ou paiement
- Frais caches jusqu'au dernier ecran
- Refus formule de facon culpabilisante
- Annulation cachee ou uniquement via support
- Suppression de donnees sans confirmation explicite
- Timer ou rarete artificielle
- Publicite deguisee en contenu ou notification
- Option payante ajoutee automatiquement

Tout red flag doit etre corrige avant livraison.

---

## Formulations recommandees

| Situation | Eviter | Preferer |
|---|---|---|
| Refus newsletter | Non, je ne veux pas d'avantages | Non merci |
| Essai gratuit | Commencer | Commencer l'essai gratuit - puis 12 EUR/mois |
| Suppression | OK | Supprimer definitivement |
| Tracking | Ameliorer mon experience | Accepter les cookies d'analyse |
| Annulation | Continuer | Garder mon abonnement |

---

## Test simple

Se poser cette question :

> Est-ce que je serais a l'aise d'expliquer ce choix de design a l'utilisateur concerne, en face a face ?

Si la reponse est non, le pattern doit etre modifie.
