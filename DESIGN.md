# DESIGN — Météo (gameday-meteo)

> Journal de design tenu par Claude (prompt design, `PROMPT-DESIGN.md`). Versions datées, jamais écrasées.
> Livrables : `G-DESIGN/` (`PAGES.md`, `REFS.md`, `STYLE.md` à venir, `STYLE.md`, `planches/v1|v2|v3/*.html`).

## LOCK — 2026-11-18 · style verrouillé

Gaia a validé les 4 planches V3 et demandé `/lock`. Fin des explorations.

- **Style de référence** : `G-DESIGN/STYLE.md` (Bulletin trame : deux encres riso, trames à points variables, buée et profondeur de champ).
- **Planches validées** : `G-DESIGN/planches/v3/` — 01 Post, 02 Jeu, 03 Carte de fin, 04 Séries & classement.
- V1 (`planches/v1/`) et V2 (`planches/v2/`) restent archivées, non retenues.
- **Toujours ouvert côté produit** (ne bloque pas le style, mais bloque l'implémentation) : nature exacte de la prévision, nombre d'essais, score juste/faux ou « proche », et si le jeu connaît les témoignages décisifs (bloc « What gave it away » de la carte de fin). Voir `G-DESIGN/PAGES.md`.
- Prochaine étape du pipeline : implémentation du design dans l'app Devvit (prompt 07b-impl-design), en suivant `STYLE.md`.

### Changelog
- 2026-11-18 · LOCK · 4 pages validées, style verrouillé.

## V3 (suite) — 2026-11-18 · déclinaison des pages

**Statut** : style Bulletin trame validé par Gaia (« Oui, décline »), puis pages validées au LOCK.

### Fait
- `G-DESIGN/STYLE.md` : encres, trames (pas, angles, rayons), règles net/flou et buée, typo, grille, composants, états, mouvement, interdits.
- `planches/v3/01-post.html` — **Post** : la même rue, rideaux tirés devant des fenêtres allumées (on sait que six voisins ont vu le ciel, pas ce qu'ils ont vu), compteur du matin, taux de réussite, « Open the windows ».
- `planches/v3/03-carte-de-fin.html` — **Carte de fin** : la vignette de la rue reçoit sa trame de bruine, tampon « Spot on / Not today », série et semaine en petits ciels, indice décisif, répartition des prévisions en barres tramées (la tienne en jaune), « commenter sans spoiler », « copier mon bulletin », prochain matin.
- `planches/v3/04-series-classement.html` — **Séries & classement** : calendrier du mois en cases imprimées (trouvé jaune / raté bleu / absent pointillé), série, meilleure série, taux, classement des plus longues séries de la rue.

### Hypothèses produit appliquées (toujours ouvertes dans PAGES.md)
Score juste/faux, un seul essai par jour. « What gave it away » suppose que le jeu sait quels témoignages sont décisifs : à confirmer, sinon on retire le bloc.

### Corrections
- Dates de démo : le 18/11/2026 est un **mercredi** (V1/V2 disaient « Tue » ; corrigé en V3, V1/V2 restent archivées telles quelles).

### Changelog
- 2026-11-18 · V3 · STYLE.md + planches Post, Carte de fin, Séries & classement.

## V3 — 2026-11-18 · Bulletin renforcé (trame + net/flou)

**Statut** : en revue. Gaia a retenu la direction B (Bulletin) et demandé : renforcer le pointillisme, ajouter du flou/net « comme une goutte de pluie qui rend flou ce qu'il y a derrière ».

Planche : `G-DESIGN/planches/v3/02-bulletin-trame.html` (V2 conservée).

### Décisions
- **Vraie trame à points variables** (la taille du point suit la tonalité), calculée point par point : ciel d'aube jaune qui s'épaissit vers les toits, façade modelée par une lumière venue de la gauche, lampe de Sam qui rayonne, rue qui fonce vers le spectateur. Bleu tramé à 15°, jaune à 75° (angles de riso deux tambours). Plus aucun aplat de couleur hors texte et filets.
- **Silhouettes des voisins en encre pleine** : en trame, les indices (lunettes, géraniums) devenaient illisibles. Lisibilité du jeu avant l'effet.
- **Net / flou** : on regarde la rue à travers sa propre vitre. Les bords de la vue passent hors champ, les toits du fond sont en bokeh, et 11 gouttes de buée grossissent et floutent ce qu'elles recouvrent (vraie réfraction : copie agrandie et floutée de la scène sous chaque goutte). Le texte (bulles, boutons) reste toujours net, au-dessus.
- **Buée, pas pluie** : les gouttes sont là tous les matins, quel que soit le ciel du jour, sinon elles souffleraient la réponse. **Validé par Gaia le 2026-11-18.**
- Technique : effet fait en SVG pur (`<use>` + flou + masque), pas en `backdrop-filter`, qui ne s'affichait pas au rendu de contrôle et reste fragile. Portable tel quel dans le post Devvit.
- États dessinés : goutte en gros plan, survol d'une voix (sa fenêtre nette, la voisine floue), cases repos/survol/cochée en trame, bouton inactif.

### Changelog
- 2026-11-18 · V3 · Bulletin trame : trame AM, gouttes de buée, profondeur de champ, états net/flou.
- 2026-11-18 · V3 · Gaia valide la buée présente chaque matin (indépendante du ciel du jour).

## V2 — 2026-11-18 · refonte de la page Jeu (desktop seul)

**Statut** : en revue, j'attends la validation de Gaia.

### Retour de Gaia sur V1
« Slop IA : la matière, les couleurs, les motifs n'ont pas été travaillés, pas d'identité visuelle. » Le mobile n'est pas utile : desktop seul sauf si le hackathon le demande. Aller voir les références jeux.

### Décisions
- **Mobile retiré.** Les critères officiels (`criteres/reddit-gameday-2026.md`) ne mentionnent ni mobile ni device ; le « mobile first » venait de l'idéation. Cela contredit le §6 de `PROMPT-DESIGN.md`, c'est Gaia qui tranche.
- **Références jeux** ajoutées à `G-DESIGN/REFS.md` (Firewatch surtout).
- **Le jeu devient une scène dessinée**, plus une grille de cartes : un immeuble, six fenêtres où l'on voit chaque voisin et son indice (lunettes au crochet, géraniums, lampe allumée…), une boulangerie au drapeau mou, des passants sous parapluie, et le ciel laissé en blanc : c'est la question. Chaque voix est une bulle reliée à sa fenêtre.
- Géométrie commune aux trois directions, seul le traitement change (couleur, matière, typo) : on compare des identités, pas des mises en page.

### Directions (`G-DESIGN/planches/v2/`)
- `01-veilleuse.html` — **Veilleuse** : rampe de 6 valeurs d'ardoise façon Firewatch, fenêtres ambre comme seule chaleur, géométrique légère espacée, boutons bannière biseautés.
- `02-bulletin.html` — **Bulletin** : risographie deux encres (bleu + jaune en surimpression décalée), trames de points, grain papier, ciel = ligne vide à remplir, condensée + mono + serif italique.
- `03-decoupage.html` — **Découpage** : diorama de papiers découpés avec ombres portées et fibre, façade terre cuite, témoignages en étiquettes scotchées, ciels en pastilles à soulever.

### Ma recommandation
**Veilleuse** : c'est la plus « jeu », la lumière des fenêtres raconte déjà « six voisins réveillés ce matin », et elle se démarque le mieux dans un feed clair. Bulletin a la matière la plus singulière ; Découpage est la plus chaleureuse mais la plus coûteuse à animer en prod.

### Changelog
- 2026-11-18 · V2 · 3 nouvelles planches (scène dessinée), mobile retiré, refs jeux, PAGES.md mis à jour. V1 conservée dans `planches/v1/`.

## V1 — 2026-11-18 · exploration de la page Jeu

**Statut** : en revue, j'attends la validation de Gaia (étape B du process). Rien n'est décliné.

### Fait
- Références ouvertes et décodées : `G-DESIGN/REFS.md` (Concept Studio : flat, 3 marches typo, étiquette mono ; Craft : surface douce, soin du texte, un seul bouton plein).
- Pages proposées : `G-DESIGN/PAGES.md` (Post, Jeu, Carte de fin, Séries & classement) + 5 questions produit ouvertes.
- 3 planches de la page Jeu, chacune en desktop 1440 × 900 et en mobile 390 × 844 dans un feed neutre (sans marque), avec une rangée d'états (repos, survol, choisi, CTA inactif, envoi, chargement) :
  - `01-facade.html` — **Façade** : la direction du brief. Six fenêtres au trait sur un mur clair, flat, accent soleil.
  - `02-carnet.html` — **Carnet** : six petits mots en serif sur papier chaud, mini-fenêtre en signature, panneau de prévision séparé, accent bleu pluie.
  - `03-lucarne.html` — **Lucarne** (écart) : une grande croisée à six carreaux sur un mur d'aube, le verre prend la teinte du ciel choisi, accent soleil.

### Décisions
- Mêmes données de démo sur les trois planches (Morning 042, Linden Row, 6 voisins, 6 ciels, choix « Drizzle ») pour comparer le style, pas le contenu.
- Une seule couleur d'accent par direction (soleil en 01 et 03, pluie en 02).
- Contraste vérifié (WCAG AA ≥ 4,5:1) sur les textes : ont été ajustés le voile de 02 (`#eef3f9`), son gris secondaire (`#646d79`) et le verre « Cloudy » de 03 (`#65717e`).
- Polices : piles système / libres uniquement (Nunito, Iowan/Charter, Futura/URW Gothic en tête de pile) ; à embarquer en prod (CSP).
- Le jeu est dessiné tel qu'`IDEE.md` le permet ; tout ce qui n'y est pas est listé en questions dans `PAGES.md` (nature de la prévision, nombre d'essais, score).

### Ma recommandation
**03 Lucarne.** Le cadre de fenêtre y est le jeu lui-même au lieu d'un décor, la lumière changeante devient le retour visuel du choix, et un post sombre se repère tout de suite dans un feed clair. 01 est la plus sûre et la plus fidèle au brief ; 02 lit le mieux mais ressemble davantage à une appli de notes qu'à un jeu.

### Changelog
- 2026-11-18 · V1 · création du journal, REFS, PAGES, 3 planches Jeu.
