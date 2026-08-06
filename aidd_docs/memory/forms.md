# Forms

How forms are built and validated across the UI.

## Approach

- **zod** pour la validation, **Server Actions** pour la soumission. Pas de bibliothèque de formulaire imposée : les primitives React et shadcn/ui suffisent au volume du projet.
- Le schéma d'un formulaire vit dans `src/features/<feature>/schemas/`, **jamais** dans le composant.
- La stratégie zod d'ensemble — ses cinq frontières et la règle du schéma unique — est décrite dans [`architecture.md`](architecture.md).

## Conventions

- Une Server Action valide toujours ses entrées avec **`safeParse`**, pas `parse` : elle renvoie des erreurs typées que le formulaire sait afficher champ par champ.
- **L'appel depuis l'interface n'est jamais une garantie.** Une Server Action est un endpoint HTTP appelable directement : elle vérifie l'identité et les droits avant de valider la forme.
- Le même schéma sert au client et au serveur, dérivé par `.pick()` / `.omit()` / `.extend()`. Jamais recopié.
- Les erreurs s'affichent au champ concerné ; `sonner` est réservé au résultat global de l'action.
- Les mutations perçues comme instantanées — réactions, favoris — passent par `useOptimistic` : l'interface répond avant la base, et se corrige si l'action échoue.
