# Project Brief

What this project is, the problem it solves, and its domain language. The non-derivable "why", not the "how".

## What it is

- BlueOasis est un média tech francophone : guides, conventions et bonnes pratiques, en articles MDX et en vidéo.
- Public : développeurs, profils infra / réseau / système, étudiants et curieux de l'informatique, francophones.

## Why it exists

- La ressource tech de référence est anglophone. BlueOasis existe pour qu'apprendre la tech en français ne soit pas un second choix.
- Le différenciateur n'est ni le volume ni la fréquence de publication, mais **la qualité de l'expérience de lecture**.
- Cible à 6 mois : 100 à 1000 visiteurs par mois. Ce chiffre est une contrainte de conception, pas une ambition : **le sur-dimensionnement est traité comme un défaut**.

## Domain language

| Terme | Sens |
| --- | --- |
| Article | Un contenu MDX versionné dans `content/articles/`. Jamais en base |
| Série | Un parcours ordonné d'articles liés, déclaré dans `content/series/` |
| `article_id` | L'identifiant **immuable** d'un article, porté par son frontmatter. La seule clé de jointure vers la base |
| Slug | L'identifiant d'URL d'un article. **Mutable** — jamais une clé étrangère |
| Îlot dynamique | Une zone rendue au runtime dans une page par ailleurs prérendue |
| Engagement | Ce qu'un lecteur a fait sur un article : commentaires, réactions, favori, progression |
| État public | Une donnée visible de tous (compteurs de réactions) |
| État privé | Une donnée qui n'appartient qu'à son propriétaire (favoris, progression) |

## Key features

- **Contenus riches** — articles et guides en MDX, sommaire automatique, code coloré, vidéos YouTube intégrées.
- **Recherche instantanée** — plein texte français, résultats au fil de la frappe, sans appel réseau.
- **Communauté** — commentaires, likes et réactions, avec modération.
- **Interactivité UI/UX** — palette de commandes, transitions, réactions optimistes, progression de lecture. *Jamais de l'exécution de code : ce périmètre a été écarté explicitement.*
- **Parcours de lecture** — séries et collections, favoris, reprise de lecture.
- **Administration** — file de modération, signalements, gestion des comptes, journal d'audit.
