# KarmaVer$e — Event Leaderboard

Public, no-login leaderboard page for KarmaVer$e events. Opens on a QR scan and
shows the top 10 users by Karma Coins earned. Single self-contained `index.html`
(no build step, no dependencies).

## Backend
Reads a public endpoint:

```
GET <BACKEND_HOST>/api/v1/leaderboard/event          # normal load (may be cached ~30s)
GET <BACKEND_HOST>/api/v1/leaderboard/event?force=true   # Refresh button (bypass cache)
```

Default host is **production** (`https://karmacoin-backend-productionn.onrender.com`).
Override without editing the file by appending `?api=` to the page URL, e.g.

```
https://<pages-url>/?api=https://staging-host
```

Response shape (top 10, already sorted desc):

```json
{ "success": true, "data": [ { "rank": 1, "name": "Sachin Kumar", "coins": 777 } ] }
```

## Features
- Top 3 podium (🥇🥈🥉) + ranks 4–10 list
- Refresh button (`force=true`), loading / empty / error states
- Silent auto-refresh every 60s (pauses when the tab is hidden) — rate-limit friendly
- Mobile-first, KarmaVer$e green + gold theme, names HTML-escaped

## Hosting
Any static host works (GitHub Pages, Netlify, Vercel, or a backend route).
The backend must allow **CORS** for the page's origin, since the page fetches the
API from the browser.

## Local preview
Just open `index.html` in a browser. (Cross-origin fetch to the backend needs the
backend's CORS to permit the origin — `file://`/localhost may be blocked depending
on backend config.)
