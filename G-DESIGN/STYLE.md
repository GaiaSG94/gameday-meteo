# STYLE — Météo · « Bulletin trame »

> **Verrouillé (/lock) le 2026-11-18.** Fin des explorations : toute évolution passe par `/delta` sur ce style. Style validé par Gaia (direction B, V3). Référence de vérité : `planches/v3/02-bulletin-trame.html`.
> Desktop uniquement (post Reddit dans le feed, cadre 1440 × 900).

## 1. Idée

Le bulletin météo de la rue, imprimé en risographie deux encres, qu'on lit à travers sa propre vitre embuée. Toute la matière vient de l'impression : deux encres, des trames de points, le grain du papier, le léger décalage entre les passages. La profondeur vient de l'optique : net au centre, flou au fond et sous les gouttes de buée.

## 2. Encres et papier

| Rôle | Hex | Usage |
|---|---|---|
| Papier | `#f1ebdf` | fond de tout le jeu, intérieur des bulles et des cases |
| Encre bleue (riso Medium Blue) | `#2b4ea2` | texte, filets, silhouettes, trames d'ombre |
| Encre jaune (riso Yellow) | `#ffd23f` | lumière : fenêtres, sélection, ombres portées tramées, CTA (texte) |
| Surimpression | `#a7b03d` | jamais posée en aplat : elle naît du jaune multiplié sur le bleu |
| Bleu éteint | `#7d93c9` | uniquement états inactifs (contraste 2,6:1, réservé au désactivé) |
| Crème sur bleu | `#fff4c4` | petit texte secondaire sur le CTA bleu |

Règles :
- **Deux encres, pas une de plus.** Le jaune passe toujours en `mix-blend-mode: multiply`.
- **Aucun aplat de couleur** hors texte, filets, silhouettes et CTA. Tout le reste est une trame.
- Contrastes mesurés : bleu / papier 6,5:1 ; jaune / bleu 5,4:1 ; crème / bleu 7,0:1.

## 3. Trames

| Trame | Encre | Angle | Pas | Rayon | Usage |
|---|---|---|---|---|---|
| `b1` | bleu | 15° | 5 px | 0,85 | voisins du fond, rideaux, survol |
| `b2` | bleu | 15° | 5 px | 1,35 | toits lointains, vitrine, ombre des gouttes |
| `b3` | bleu | 15° | 4,4 px | 1,95 | corniche, cheminée, bandeaux |
| `bs` | bleu | 15° | 3,6 px | 1,7 | parapluies, passants |
| `y1` | jaune | 75° | 5 px | 1,2 | fenêtres des voisins du fond |
| `y2` | jaune | 75° | 5 px | 2,05 | vitres allumées, drapeau, auvent, sélection |
| CSS `--dotY` | jaune | 0° | 4,6 px | 1,55 | ombres portées des bulles et du CTA, case cochée |
| CSS `--dotB` | bleu | 0° | 4,6 px | 0,9 | bandeau du titre, survol de case, barres |

**Trame à points variables** (taille du point = tonalité) pour tout ce qui a un dégradé : ciel d'aube (jaune, s'épaissit vers les toits), façade (bleu, lumière venue de la gauche), lampe (jaune radial), rue (bleu, fonce vers le spectateur). Générée point par point ; jamais de `linear-gradient` visible.

**Décalage de repérage** : le jaune des vitres est décalé de (1,6 ; 1,2) px par rapport au bleu. Les icônes ont une ombre jaune de (1,6 ; 1,2) px.

## 4. Net / flou

- **Profondeur de champ** : les bords de la vue (masque radial, 72 % → 100 %) sont floutés à 2 px ; les toits du fond à 2,6 px, les voisins à 1,6 px. L'immeuble central reste net.
- **Buée** : 11 gouttes sur la vitre du joueur, de 16 à 52 px. Chaque goutte montre la scène derrière elle **agrandie ×1,7 et floutée à 2,6 px**, avec un liseré bleu en bas, un reflet papier en haut à gauche et une ombre tramée `b2` décalée de (1,5 ; 2,5).
- **La buée est là chaque matin, quel que soit le ciel du jour** (validé Gaia) : elle n'est jamais un indice.
- Jamais de goutte sur une fenêtre de voisin, sur une bulle ou sur un texte.
- **Le texte n'est jamais flou** : bulles, boutons, chiffres sont au-dessus de la vitre.
- Implémentation : SVG pur (`<use href="#world">` + `feGaussianBlur` + masque/clip). Pas de `backdrop-filter`.

## 5. Typographie

| Rôle | Pile | Taille / graisse | Détails |
|---|---|---|---|
| Titrage (masthead, CTA, tampons, ciels) | Nimbus Sans Narrow → Arial Narrow → Helvetica Neue | 34 / 700 (masthead), 22 / 700 (CTA), 12 / 700 (cases) | capitales, approche −0,01 à +0,06 em |
| Étiquettes, chiffres, métadonnées | DejaVu Sans Mono → Liberation Mono | 10–11 / 400–700 | capitales, chiffres tabulaires |
| Voix des voisins | Iowan Old Style → Charter → Georgia | 14,5 / 400 italique, interligne 1,26 | guillemets typographiques |
| Très grands chiffres (série, %) | titrage condensé | 56–64 / 700 | chiffres tabulaires |

En prod, embarquer des équivalents libres (Archivo Narrow, IBM Plex Mono, Source Serif) : aucune requête externe (CSP).

## 6. Grille

- Zone de jeu **740 px** de large dans le post (colonne feed 772 px).
- Marges intérieures 22 px ; masthead 56 px, filet double bleu 3 px dessous.
- Scène 740 × 420 : immeuble centré (x 250–490), bulles à 14 px du bord, largeur 226 px, filets pointillés de 32 px jusqu'à la fenêtre.
- Rangée de 6 cases (gouttière 10 px), puis CTA pleine largeur 54 px.

## 7. Composants

- **Masthead** : « MÉTÉO » en titrage + ligne mono (bulletin, numéro, date) ; à droite, cellules mono séparées par des filets bleus.
- **Bulle de voix** : papier, filet bleu 1,5 px, étiquette mono « 3A · MARGIT », citation en serif italique ; ombre jaune tramée décalée de 5 px ; filet pointillé vers sa fenêtre.
- **Case de ciel** : filet bleu 1,5 px, icône au trait 2,2 px + ombre jaune décalée, libellé titrage.
- **CTA** : aplat bleu, texte jaune en titrage, mention mono crème ; ombre jaune tramée décalée de 6 px.
- **Tampon** : cadre double bleu, texte titrage, fond jaune tramé, incliné de −6°, léger décalage de repérage.
- **Barre de répartition** : trame `--dotB` dont la longueur suit le pourcentage ; la barre du joueur en trame jaune.
- **Ligne à remplir** : texte titrage + filet bleu ; une fois remplie, la réponse y est « imprimée ».

## 8. États

| Élément | Repos | Survol | Actif / choisi | Inactif | Chargement |
|---|---|---|---|---|---|
| Case de ciel | papier + filet | trame bleue `--dotB` | trame jaune + filet intérieur | — | — |
| Bulle | nette | sa fenêtre nette, le reste de la scène passe en flou | — | — | cadre pointillé, lignes vides |
| CTA | bleu + ombre jaune | ombre qui se réduit de 2 px | « Printing… » | papier, cadre pointillé bleu éteint, sans ombre | — |
| Fenêtres | allumées (trame jaune) | — | — | — | rideaux tirés (trame bleue) |

## 9. Mouvement

- **Impression** : à l'ouverture, le bleu apparaît d'abord, puis le jaune 120 ms après, avec un décalage de repérage qui se stabilise (2 px → 1,6 px) en 200 ms.
- **Révélation du ciel** (carte de fin) : la trame du vrai ciel s'imprime de haut en bas en 600 ms, puis le tampon tombe (échelle 1,15 → 1, 180 ms).
- **Buée** : immobile. Pas de goutte qui coule : ce serait de la pluie.
- **Survol** : passage net / flou en 160 ms.
- Respect de `prefers-reduced-motion` : tout apparaît d'un coup.

## 10. Interdits

Troisième encre, aplats de couleur décoratifs, dégradés lisses visibles, texte flou, goutte qui coule, emoji, Snoo ou karma, police chargée depuis le réseau.
