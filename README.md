# Akış Bilinci — observations-app (Safe Build)

- Next.js 13.4.4 (pages router) + TypeScript + Tailwind
- Prisma + PostgreSQL
- **Safe build**: `DATABASE_URL` boşsa `db push` atlanır; build düşmez.
- `/api/health`: ENV yoksa 200 + `{ ok:false }` döner.

## Hızlı Başlangıç
```
cp .env.example .env   # Windows'ta içeriği manuel kopyalayın
# .env -> DATABASE_URL doldurun (örn: postgresql://.../db?sslmode=require)

npm install
npm run prisma:generate
npm run prisma:push
npm run dev
```

## Vercel
- Env → `DATABASE_URL` ekle (Vercel Postgres/Neon). İstersen `&schema=akisb` kullan.
- Redeploy: `vercel-build` otomatik `db push` çalıştırır (env varsa).

## Doğrulama
```
curl -s https://<domain>/api/health
curl -X POST https://<domain>/api/observations -H "Content-Type: application/json" -d '{"category":"iş","text":"Prod deneme","user":"B"}'
curl -s https://<domain>/api/observations | head
```
