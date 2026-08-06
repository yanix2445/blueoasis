# Auth

How identity and access work: authentication and authorization.

## Authentication

- **BetterAuth**, instancié dans `src/server/auth/betterauth.ts`, exposé par le Route Handler `/api/auth/[...all]`.
- Adaptateur Drizzle sur la base Postgres — voir [`database.md`](database.md) pour la contrainte de driver, qui conditionne la création d'utilisateur.
- Emails transactionnels délégués à Resend — voir [`integration.md`](integration.md).
- Le compte n'est pas là que pour les commentaires : favoris et progression de lecture sont de l'état par utilisateur.
- **Épingler une version corrigée.** Des failles de prise de contrôle de compte ont été publiées ; les plugins optionnels non utilisés (SSO, SCIM, facturation, fournisseur OAuth) ne doivent pas être installés « au cas où ». Les numéros exacts sont dans [`../INSTALL.md`](../INSTALL.md).

## Authorization

Deux rôles seulement : lecteur et administrateur, via le plugin `admin` de la bibliothèque.

**Les cinq règles de la zone d'administration :**

1. **Le rôle se vérifie dans chaque Server Action et chaque query — jamais uniquement dans le layout.** Un layout est de l'affichage ; une Server Action est un endpoint HTTP appelable directement. `requireAdmin()` vit dans `src/server/auth/guards.ts` et s'appelle partout. *C'est le mode d'échec réellement observé dans les failles publiées de cette bibliothèque : un endpoint sans contrôle de rôle à côté de dix endpoints protégés.*
2. Le proxy est une redirection rapide, pas une autorisation — voir [`navigation.md`](navigation.md).
3. Les zones protégées sont exclues de l'indexation — voir [`navigation.md`](navigation.md).
4. **Chaque mutation de modération écrit dans `moderation_log`** : qui, quoi, sur quoi, pourquoi, quand.
5. **Aucune cible n'est acceptée sur parole.** L'identifiant venant du client est validé par zod, puis relu en base avec vérification du droit, avant toute écriture.

Le premier compte administrateur est promu **manuellement en base**. Aucune interface ne permet l'auto-promotion.

## Sessions

- Session par cookie, gérée par la bibliothèque. Lecture centralisée dans `src/server/auth/session.ts` (`requireUser()`).
- Le proxy ne fait que constater la présence du cookie ; la session n'est validée que côté serveur, dans les Server Components, Server Actions et Route Handlers.

## Suppression de compte (RGPD)

Choix retenu : **anonymiser l'auteur, conserver le texte, purger sur demande explicite.**

| Donnée | Traitement |
| --- | --- |
| `comment` | `user_id` mis à `NULL`, horodatage d'anonymisation. **Texte conservé**, affiché « Compte supprimé » |
| `reaction`, `bookmark`, `reading_progress` | Supprimés |
| Signalements émis | Anonymisés |
| `moderation_log` | **Conservé** — l'acteur y est un administrateur, et c'est la preuve de conformité |

Sur demande explicite de purge, les commentaires sont réellement supprimés et remplacés par une pierre tombale, pour que les réponses gardent leur sens.

⚠️ Si un compte supprimé était la **cible** d'une action de modération, le journal en garde la trace. C'est légitime, mais **doit être déclaré dans la politique de confidentialité**.
