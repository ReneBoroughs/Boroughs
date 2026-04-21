# Créer une base de données hébergée chez Vercel (guide rapide)

Ce guide explique la mise en place d'une base **Vercel Postgres** et son utilisation dans une app web.

## 1) Créer la base sur Vercel
1. Ouvre ton dashboard Vercel.
2. Va dans **Storage**.
3. Clique **Create Database** puis choisis **Postgres**.
4. Sélectionne le projet, la région et valide.

## 2) Lier la base au projet
1. Dans l'onglet de la base, clique **Connect Project** (si ce n'est pas déjà fait).
2. Vercel ajoute automatiquement les variables d'environnement au projet (Preview / Production).
3. Vérifie au minimum :
   - `POSTGRES_URL`
   - `POSTGRES_PRISMA_URL`
   - `POSTGRES_URL_NON_POOLING`
   - `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DATABASE`, `POSTGRES_HOST`

## 3) Utiliser la base dans le code

### Option A — Prisma
```bash
npm i prisma @prisma/client
npx prisma init
```

Puis dans `prisma/schema.prisma`, configure `DATABASE_URL` vers `POSTGRES_PRISMA_URL`.

Migration :
```bash
npx prisma migrate dev --name init
```

### Option B — SQL direct (package `@vercel/postgres`)
```bash
npm i @vercel/postgres
```

Exemple :
```ts
import { sql } from '@vercel/postgres';

export async function getUsers() {
  const { rows } = await sql`SELECT id, email FROM users LIMIT 20`;
  return rows;
}
```

## 4) Déploiement
1. Push ton code.
2. Déploie sur Vercel.
3. Vérifie que les variables d'environnement existent en Preview et Production.

## 5) Vérification rapide
- Exécuter une requête simple (`SELECT 1`).
- Vérifier la connectivité depuis l'environnement de déploiement (pas uniquement en local).
- Confirmer que les migrations ont bien été appliquées.

## Note sur « voir le chat Site IML »
Je ne peux pas voir directement un chat externe ou une interface privée (comme un chat de ton site) sans contenu partagé ici.

Si tu veux, colle :
- le lien public (si accessible),
- ou les erreurs affichées,
- ou le code du composant de chat,

et je te guide étape par étape pour corriger le flux (affichage du prompt, focus input, état de streaming, etc.).
