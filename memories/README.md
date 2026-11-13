# Couple Memories ❤️

A private photo/video platform for two people. React + Vite, Express + Mongoose, MongoDB, Cloudinary, Docker.

## Run with Docker
1. `cp .env.example .env`, then set both `JWT_*` secrets and your Cloudinary credentials.
2. `docker compose up --build`
3. Open http://localhost:5173 (API health: http://localhost:5173/api/health)

## Run without Docker
```bash
# backend
cd backend && cp .env.example .env && npm install && npm run dev
# frontend (proxies /api to localhost:5000)
cd frontend && npm install && npm run dev
```
Tests: `cd backend && npm test`

## Features
**Memories**: multi-file drag & drop upload with progress, per-photo date (or choose one), title, caption, location, tags; edit any detail; full-screen viewer with keyboard navigation; download; favorites (personal to each partner); emoji reactions; comments.
**Delete safely**: delete moves to Trash (restorable for 30 days, auto-purged), permanent delete, empty Trash, bulk delete.
**Find things**: search, filter by photo/video, tag, date range, favorites; sort; pagination; Mine / Partner's / Ours tabs.
**Organise**: albums (create, edit, cover, add/remove, bulk), timeline grouped by month, "On this day".
**Our dates**: anniversary counter, birthdays, trips, recurring events, countdowns.
**Together**: notifications (uploads, comments, reactions, partner joined), invite code with regenerate/cancel.
**Account**: profile + avatar, change password, forgot/reset password, email verification, sign out everywhere, leave space, delete account.
**Dashboard**: days together, totals, storage, uploads per month, top tags, upcoming dates.

## Production hardening included
Short-lived access token + rotating refresh token with reuse detection; hashed tokens at rest; bcrypt; rate limiting; helmet; Origin check on mutating requests; zod validation on every input; signed Cloudinary URLs for private (`authenticated`) media; upload type allow-list and disk-streamed uploads; graceful shutdown; health/readiness endpoints; non-root Docker image.

## Before going public
- Serve over HTTPS and set `COOKIE_SECURE=true`.
- Configure SMTP so verification/reset emails really send.
- Add backups for MongoDB, error monitoring, and API integration tests (the included tests cover the pure logic only).
- Signed Cloudinary URLs are unguessable but do not expire; for expiring links use Cloudinary token-based delivery.
- Memories uploaded with the old starter remain public-type assets until re-uploaded.
