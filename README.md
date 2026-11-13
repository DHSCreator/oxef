# OXEF — Lead Operations Platform

A B2B/B2C lead automation dashboard: one place where leads from your website form, email, Instagram (DMs + comments), and Telegram bot land, get tagged, followed up, and booked.

## Stack
- **Next.js 16** (App Router) — UI + API routes
- **Drizzle ORM + better-sqlite3** — local file DB, zero external services to start. Swap to Postgres later (see below) without touching the schema much.
- **NextAuth v5** (Auth.js) — email/password login (credentials provider), JWT sessions
- **Tailwind CSS 4**

## What's built
- `/api/intake` — the single front door for inbound leads from **any** channel (website form, email parser, Instagram DM/comment bot, Telegram bot). Protected by `INTAKE_API_KEY` sent as `x-api-key` header.
- `/api/leads`, `/api/leads/[id]`, `/api/leads/[id]/booking` — internal API used by the dashboard (session-protected)
- `/dashboard` — overview with lead counts (new / follow-up / booked / won)
- `/dashboard/leads` — CRM table, filterable by `?mode=B2B` or `?mode=B2C`
- `/dashboard/leads/[id]` — lead detail: status changer, notes, booking scheduler, full activity log
- Auth: `/login`, middleware-protected `/dashboard/*`

## Running it locally
```bash
npm install
npm run db:push        # creates the sqlite tables
npm run db:seed        # creates an admin user + 2 sample leads
npm run dev
