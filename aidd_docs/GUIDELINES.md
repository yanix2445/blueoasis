# AI Operating Guidelines

How this team drives AI coding assistants on this project. Keep it short and specific to this repo.

BlueOasis est développé **en solo**. Ces règles compensent l'absence de relecteur humain.

## House rules

- **Ne jamais introduire une dépendance sans vérifier qu'elle est maintenue** — date de dernière publication npm et activité des commits. Deux bibliothèques ont déjà été écartées à ce titre pendant la conception. Une dépendance abandonnée est un défaut, pas un détail.
- **Le rôle et l'identité se vérifient dans chaque Server Action**, jamais seulement dans un layout ou le proxy. Voir [`memory/auth.md`](memory/auth.md).
- **Une feature n'importe jamais un fichier interne d'une autre feature** — uniquement son `index.ts`.
- **Ne jamais éditer à la main** : `drizzle/` (migrations générées), `.velite/`, `public/pagefind/`, et le bloc `<aidd_project_memory>` des fichiers de contexte.
- **Aucune couleur, aucune URL, aucun domaine en dur.** Les tokens vivent dans le thème, le domaine dans une variable d'environnement.
- Les commits restent atomiques et disent l'intention. Convention dans [`memory/vcs.md`](memory/vcs.md).
- **Rester dimensionné pour le trafic réel** : 100 à 1000 visiteurs par mois. Une solution qui « scale » mais alourdit le développement est un mauvais choix ici.

## Validation depth

- Changement de contenu MDX uniquement : le build suffit — la validation du frontmatter est le garde-fou.
- Changement de code : la barrière rapide de [`memory/coding-assertions.md`](memory/coding-assertions.md).
- Touche à l'auth, à la modération ou aux données personnelles : **relecture complète obligatoire**, plus un test qui couvre le cas d'autorisation. Ce sont les zones où une erreur ne se voit pas à l'écran.
- Avant une fusion : types, lint, tests et build au vert.

## When the AI drifts

- Réinitialiser la session et réénoncer l'objectif en une phrase.
- Si la proposition contredit un fichier de `memory/`, **c'est la mémoire qui fait foi** — ou elle est périmée, et il faut la corriger d'abord, pas la contourner.
- Si une décision d'architecture semble manquante, la chercher dans [`INSTALL.md`](INSTALL.md) avant d'en inventer une.

For the general AIDD playbook (planning, review loops, prompting and context hygiene, anti-patterns), see the framework docs: <https://github.com/ai-driven-dev/framework>.
