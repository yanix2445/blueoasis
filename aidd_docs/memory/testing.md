# Testing

How the project is tested: the layers, the tools, and the conventions. Where tests live and how to run them.

## Strategy

- **Unitaire** — règles métier, schémas zod, services. Le gros du volume.
- **Composant** — UI et interactions isolées.
- **Intégration** — une Server Action de bout en bout, contre une base de test.
- **End-to-end** — les parcours critiques seulement : inscription, publication d'un commentaire, modération d'un commentaire, suppression de compte.

Les règles métier se testent **au niveau de la feature**, jamais uniquement à travers une page : la logique doit rester indépendante du routage.

## Tools

- **Vitest** — unitaire, composant, intégration.
- **React Testing Library** — rendu et interactions des composants.
- **Playwright** — parcours end-to-end.

## Conventions

- Tests colocalisés avec ce qu'ils vérifient : `src/features/<feature>/__tests__/`.
- `src/test/` porte le setup partagé et les fabriques de données.
- Ce qui **doit** être couvert : toute Server Action (validation *et* autorisation), les règles de mise en attente des commentaires, la stratégie d'anonymisation RGPD.
- Ce qui ne se teste pas : le rendu MDX lui-même — le build échoue déjà si le frontmatter est invalide.

## Run

- `pnpm test` — Vitest
- `pnpm test:e2e` — Playwright

## État

Aucun test n'existe à ce jour : le dépôt n'a pas encore de code. Ce fichier fixe la cible convenue.
