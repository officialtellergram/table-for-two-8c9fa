# Drop Watch

A live countdown dashboard for hard-to-book restaurant reservations. Shows each
spot's **next "reservations drop"** as a ticking timer, computed correctly in
US-Eastern time (DST-aware), with list + map views, filtering, and deep links to
Resy / Tock / OpenTable / SevenRooms.

Single static file (`index.html`) — no build step. Cities are external data
(`cities/`), so adding a city never touches the code.

## Run locally
The page fetches `cities/index.json`, so it must be **served over http** (not
opened as a `file://`). Any static server works:

```bash
npx serve -l 5055 .      # then open http://localhost:5055
# or:  python -m http.server 5055
```

(If you open `index.html` directly off disk it still runs, but falls back to the
built-in NYC-only manifest.)

## Deploy (phone-friendly, free)
It's pure static — drop the folder on any static host:

- **Vercel** — `npx vercel` in this folder, or drag-drop at vercel.com/new. (Same host the NYC API runs on.)
- **Netlify** — drag-drop the folder at app.netlify.com/drop.
- **GitHub Pages** — push to a repo, enable Pages on the branch root.
- **Cloudflare Pages** — connect the repo, build command none, output dir `.`.

## Add a city
See [`cities/README.md`](cities/README.md). Short version: drop `cities/<key>.json`
and flip one manifest entry to `{"type":"json","url":"cities/<key>.json"}`.

## Data
NYC pulls live from the unofficial [hardtobook.xyz](https://www.hardtobook.xyz) API.
Release times can change without notice — always confirm with the restaurant.
