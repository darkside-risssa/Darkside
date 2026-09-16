# DARKSIDE Risssa — Supabase PostgreSQL Edition

## Stack
- Node.js + Express
- Supabase PostgreSQL via `pg`
- bcrypt password hashing
- JWT in HttpOnly cookies
- Helmet + rate limiting
- Login IP/device/browser/OS logging
- Admin users, sessions, categories, downloads, audit logs and settings
- Cookie ↔ JSON tools process only data manually supplied to the app

## Supabase setup
1. Create a project at https://supabase.com/.
2. Open **Project Settings → Database** and copy the connection string. Prefer the transaction/session pooler connection string if your hosting provider has connection limits.
3. Set `DATABASE_URL` in your backend hosting provider. Keep it server-side; never put it in frontend code.
4. Set `JWT_SECRET`, `ADMIN_EMAIL`, and `ADMIN_PASSWORD` as backend environment variables.
5. On first startup, the server creates the required tables and default categories and creates the admin account if the configured email does not already exist.

## Local run
```bash
cd server
npm install
cp .env.example .env
# edit .env with your Supabase DATABASE_URL and secrets
npm start
```

## Netlify
Netlify can host the static frontend, but this Express backend should run on a Node-compatible backend host unless you convert its routes to Netlify Functions. The browser should call the backend API URL; do not expose DATABASE_URL or JWT_SECRET to Netlify client-side code.

## Security
- Do not commit `.env`.
- Use a long random `JWT_SECRET` and a unique admin password.
- Use HTTPS in production.
- `TRUST_PROXY=true` is appropriate when the backend is behind a trusted reverse proxy; only enable it when that is true for your deployment.
