# Coding Assertions

The checks that must pass for code to count as done. Minimal, run after every change.

Gestionnaire de paquets : **pnpm**.

## Before commit

The fast gate.

| Order | Command | Checks |
| --- | --- | --- |
| 1 | `pnpm typecheck` | Types TypeScript |
| 2 | `pnpm lint` | ESLint |

## Before push

The heavier gate.

| Order | Command | Checks |
| --- | --- | --- |
| 1 | `pnpm test` | Vitest — unitaire et composants |
| 2 | `pnpm build` | Compilation du contenu, index de recherche, build Next |
| 3 | `pnpm check:orphans` | Aucun `article_id` en base sans article correspondant dans `content/` |

## Behavior

I fix is needed, spawn 1 agent per assertion to fix (e.g typechecking / tests / rules violated on category UI = 3 agents).

## État

Ces commandes sont **la cible convenue**, pas encore câblée : le dépôt n'a pas de `package.json` à ce jour. Elles sont à créer telles quelles lors de l'initialisation du projet, et ce fichier fait foi.
