# Dark Mode (HSL Mirroring)

Créer un mode sombre efficace ne consiste pas simplement à inverser le noir et le blanc. Le système "HSL Mirroring" permet une transition logique et mathématique des couleurs.

## 1. Le Problème des Modes Sombres Traditionnels
- **Trop de contraste :** Du texte blanc pur (`#FFFFFF`) sur un fond noir pur (`#000000`) fatigue les yeux.
- **Couleurs non adaptées :** Les couleurs saturées (ex: un rouge vif) vibrent sur un fond sombre et deviennent difficiles à regarder.
- **Profondeur perdue :** Dans un mode clair, on utilise des ombres pour créer de l'élévation. En mode sombre, les ombres sont invisibles ; on doit utiliser la luminosité de la surface pour indiquer l'élévation.

## 2. La Solution : HSL Mirroring
En utilisant le format HSL (Hue, Saturation, Lightness), on peut inverser la palette de manière cohérente :

### Luminosité (Lightness)
- En mode clair, l'arrière-plan est proche de 100% L (ex: 98%), et le texte est proche de 0% L (ex: 10%).
- En mode sombre, l'arrière-plan doit être sombre (ex: 10% L à 15% L) et le texte clair (ex: 85% L à 90% L).

### Saturation
- **Règle d'or :** En mode sombre, réduisez la saturation des couleurs d'accent (bleu, rouge, etc.) pour éviter qu'elles ne vibrent ou ne soient trop agressives.

## 3. Implémentation des Surfaces
En mode sombre, plus un élément est proche de l'utilisateur (élévation), plus il doit être **clair**.

- `surface-1` (Background) : `hsl(var(--hue) 10% 10%)`
- `surface-2` (Card) : `hsl(var(--hue) 10% 14%)`
- `surface-3` (Modal/Dropdown) : `hsl(var(--hue) 10% 18%)`

## 4. Checklist Mode Sombre
- [ ] Le fond n'est pas noir pur (`#000000`), mais plutôt un gris très foncé ou teinté (`#121212`).
- [ ] Le texte n'est pas blanc pur (`#FFFFFF`), mais légèrement adouci (ex: `rgba(255, 255, 255, 0.87)`).
- [ ] Les couleurs d'accent ont été désaturées pour rester lisibles sans agresser l'œil.
- [ ] L'élévation est représentée par l'éclaircissement des surfaces, et non par des ombres (bien que de subtiles ombres noires puissent subsister pour marquer les bords).
