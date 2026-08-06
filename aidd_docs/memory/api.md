# API

The HTTP API surface: its style, the main resources, and the contracts.

## Style

- **Pas d'API publique généraliste.** Deux surfaces distinctes, et le choix entre elles est une règle d'architecture, pas une préférence :
  - **Server Actions** — toutes les mutations déclenchées depuis l'interface. Elles vivent dans `src/features/<feature>/actions/`.
  - **Route Handlers** — uniquement pour un **contrat HTTP public**. Ils vivent dans `src/app/api/` ou à leur segment.
- **Une lecture interne ne passe jamais par HTTP.** Un Server Component appelle directement la query de la feature. Créer un endpoint interne ajoute un aller-retour réseau, une sérialisation et une surface à maintenir, sans contrepartie.
- Pas de versionnement : aucun client externe ne consomme cette surface.

## Resources

Les seuls Route Handlers légitimes du projet :

- `/api/auth/[...all]` — la surface d'authentification, déléguée à la bibliothèque d'auth. Voir [`auth.md`](auth.md).
- `/api/health` — sonde de disponibilité.
- `/rss.xml` — flux de syndication, généré depuis le contenu compilé.

`sitemap.ts` et `robots.ts` ne sont pas des Route Handlers mais des fichiers de métadonnées de la convention App Router. Ils n'ont pas de contrat à documenter ici.

## Contracts

- **Toute entrée est validée par zod avant traitement**, dans le Route Handler comme dans la Server Action. Voir [`architecture.md`](architecture.md) pour la stratégie d'ensemble.
- Une Server Action renvoie un résultat typé — succès ou erreurs par champ — jamais une exception brute destinée à l'affichage.
- Un Route Handler est **public par construction** : identité, droits, validation et gestion d'erreur y sont obligatoires, quelle que soit l'origine apparente de l'appel.
- Pas de pagination côté API : les listes d'articles sont prérendues, et les commentaires se chargent par fil.
