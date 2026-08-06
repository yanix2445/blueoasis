# Design

The visual language: the design system, tokens, and UI conventions. What it looks like, not how it is coded.

## System

- **shadcn/ui** — les composants sont copiés dans `src/shared/ui/`, donc **modifiables et versionnés**. Ce n'est pas une dépendance à mettre à jour, c'est du code du projet.
- **Tailwind CSS** — classes utilitaires. Pas de CSS-in-JS, pas de modules.
- **Thème clair / sombre** via `next-themes`.

## Tokens

- Couleurs, espacements et typographie : variables CSS dans `src/app/globals.css`, consommées par la configuration Tailwind.
- Un seul jeu de tokens, décliné par thème. Aucune couleur en dur dans un composant.

## Components

- `src/shared/ui/` : les primitives shadcn/ui. **Ne portent aucune logique métier.**
- Un composant qui commence à connaître le domaine (article, commentaire, réaction) migre vers sa feature.
- `src/features/articles/components/mdx/` : les composants exposés au MDX (blocs de code, encarts, quiz, schémas, vidéo). Ce sont eux qui rendent le contenu interactif.

## Interaction

L'expérience de lecture est le différenciateur du produit. Les briques retenues :

- `motion` — transitions et animations.
- `cmdk` — palette de commandes ⌘K, qui fusionne recherche et navigation.
- `sonner` — notifications.
- `vaul` — tiroirs mobiles. **Mobile first** : pas de menus déroulants de bureau rétrécis.
- View Transitions natives, animations au défilement en CSS pur — pas de JavaScript quand le navigateur sait faire.

## Accessibility

- Contraste et gestion du focus conformes aux primitives shadcn/ui (Radix) — ne pas les contourner.
- Les blocs de code et les schémas défilent horizontalement **dans leur propre conteneur** : la page ne défile jamais latéralement.
- Les vidéos intégrées gardent un ratio fluide et un titre accessible.
