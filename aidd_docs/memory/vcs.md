# VCS

The version-control conventions this project follows: branches, commits, and the platform.

## Setup

- Main branch: `main`
- Platform: `github`
- Ticketing: `none`

## Branches

- Format: `type/description-courte`
- Types in use: `feat`, `fix`, `chore`, `docs`, `refactor`, `test`

## Commits

- Convention: Conventional Commits — <https://www.conventionalcommits.org>
- Format: `type(scope): description`
- Rules: mode impératif, minuscules, pas de point final. Le `scope` est le nom de la feature (`comments`, `search`, `moderation`) ou une zone (`content`, `db`, `ci`).

## Commit Strategy

AI should auto commit: `after phase`

## Notes

- Le dépôt n'a **aucun commit** à ce jour : la branche `main` existe mais est vide.
- `content/` est versionné avec le code : un article se relit et se révise en pull request, comme du code.
- `drizzle/` (migrations) est versionné. `.velite/`, `public/pagefind/` et `.next/` sont générés — jamais commités.
- **`CLAUDE.md` et `AGENTS.md` sont un lien physique** — un seul fichier, deux noms. Un lien symbolique avait été essayé puis abandonné : l'éditeur ne détectait pas le changement sur le second nom et écrasait le fichier avec un tampon périmé. **Git ne conserve pas les liens physiques** : après un clone, refaire `rm AGENTS.md && ln CLAUDE.md AGENTS.md`, sinon les deux fichiers divergent en silence.
