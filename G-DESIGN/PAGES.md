# PAGES — Météo

> Statuts : à dessiner / en revue / validée. **Style verrouillé (/lock) le 2026-11-18 : les 4 pages sont validées.**
> Planches en desktop 1440 × 900 uniquement (décision Gaia V2 : les critères officiels du hackathon ne demandent pas de mobile).

| # | Page | Rôle | Contenu clé | Statut |
|---|------|------|-------------|--------|
| 1 | **Post** | Vue dans le feed : donner envie d'ouvrir le matin du jour | En-tête du post, n° du matin, façade aux 6 fenêtres encore fermées, nombre de voisins ayant déjà prévu, série du joueur, bouton « Open the windows » | **validée** · `planches/v3/01-post.html` |
| 2 | **Jeu** | Écran principal, une seule règle : « Six neighbors describe the sky. Pick one forecast. » | 6 témoignages (un par fenêtre, à meneaux), 6 ciels possibles en icônes, sélection, bouton « Forecast » | **validée** · `planches/v3/02-bulletin-trame.html` |
| 3 | **Carte de fin** | Résultat + boucle quotidienne + accroche commentaire | Juste / faux, le vrai ciel, l'indice décisif, série, % de la communauté qui a trouvé, répartition des prévisions, bouton commenter sans spoiler, prochain matin dans HH:MM | **validée** · `planches/v3/03-carte-de-fin.html` |
| 4 | **Séries & classement** | Montrer la communauté et la série | Série perso (calendrier du mois en ciels), meilleure série, taux de réussite, classement des séries de la rue | **validée** · `planches/v3/04-series-classement.html` |

Les états de chargement et d'erreur seront dessinés dans la déclinaison (étape C), pas comme pages.

## Questions produit ouvertes (non tranchées — `IDEE.md` ne le dit pas)

1. **Qu'est-ce qu'une « prévision » ?** Les planches V1 supposent **un seul choix parmi 6 ciels** : Sunny, Cloudy, Fog, Drizzle, Downpour, Storm. Faut-il aussi une température ou du vent ? (Non dessiné.)
2. **Un essai ou plusieurs ?** Les planches supposent **une seule prévision par jour** (« Forecast » verrouille). Autre option : 3 essais avec un témoignage supplémentaire révélé à chaque erreur — c'est une feature, je ne l'ai pas dessinée.
3. **Les témoignages sont-ils tous visibles d'emblée ?** Supposé : oui, les 6 d'un coup (règle lisible en 5 s).
4. **Un voisin peut-il mentir ou se tromper ?** Supposé : non, ils sont vagues mais honnêtes ; tout le sel est dans la synthèse.
5. **Score** : juste/faux seulement, ou « proche » (Drizzle vs Downpour) ? La carte de fin en dépend.
