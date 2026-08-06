# Contributing to this project's AI context

How to add or change the context the AI relies on here. For authoring AIDD skills, agents, rules, and templates, see the framework guide: <https://github.com/ai-driven-dev/framework/blob/main/CONTRIBUTING.md>.

## Changing project memory

Add or edit a file under `aidd_docs/memory/`. See [`memory/README.md`](memory/README.md) for what belongs there and how it loads.

## Adding AI content (skills, rules, agents, commands, hooks)

- Use the generator skills (`aidd-context:04-skill-generate` through `08-hook-generate`, and `10-learn` for memory or rules). They scaffold the right shape and write to the right place for each tool you use.
- Open a pull request for anything that changes how the AI behaves on this project. The team reviews it like any code change.

## Adding recipes

Create or edit project recipes under `aidd_docs/recipes/`. Use the cook skill when available so new recipes follow the shared contract and do not overwrite bundled framework recipes.

## House conventions

- **Un fait, un seul foyer.** Chaque fichier de `memory/` est propriétaire de son sujet ; les autres y renvoient par un lien au lieu de le répéter. Un fait dupliqué finit par diverger.
- **Mémoire, règle ou document ?**
  - `memory/` : ce que l'IA doit savoir à chaque session — décisions, conventions, pièges.
  - Une règle : ce que l'IA doit *faire ou ne pas faire* automatiquement en éditant du code.
  - [`INSTALL.md`](INSTALL.md) : la référence longue — comparaisons, audits, justifications. On y renvoie, on ne la recopie pas.
- **Pas de version dans un fichier de mémoire.** Nommer la technologie, pas son numéro : les numéros périment, et ils vivent dans `INSTALL.md`.
- **Pas de TODO, pas de section vide.** Un fichier de mémoire décrit l'état actuel. Ce qui reste à décider se dit en une phrase explicite, ou ne s'écrit pas.
- Les URL du produit sont en français, les identifiants de code en anglais.
