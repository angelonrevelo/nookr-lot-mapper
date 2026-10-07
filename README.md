<p align="center">
  <img src="public/nookr-wordmark.png" alt="Nookr" width="420">
</p>

# Nookr Lot Mapper

**A phone-friendly map for walking a subdivision and recording every lot — boundaries, numbers, owners — even with no signal.**

Surveying lots for an HOA usually means a printed map, a pen, and a spreadsheet typed up later. Nookr Lot Mapper puts that on your phone: open the satellite view, tap a lot to auto-trace its boundary (or draw it by hand), and fill in the lot number, block, owner and notes on the spot.

It is built for the field. Map tiles can be downloaded ahead of time so the map still works where there is no data, GPS shows where you are standing and which way you are facing, and everything you record saves on the device automatically. When you are done, export the lots as JSON or GeoJSON, or share a link straight to one lot.

## What you can do

- **Map** — satellite, street and dark tiles; tap a lot to detect its edges, or draw a polygon that snaps to them.
- **Record** — lot number, block, owner and notes per lot; search by any of them.
- **Work in the field** — GPS position with compass heading, distance and bearing to the selected lot, a quick-action button for draw / detect / GPS / undo.
- **Work offline** — installable as an app (PWA); download tiles for the area you will survey.
- **Keep your data** — auto-saved to the browser (IndexedDB), undo/redo, import, and export to JSON or GeoJSON.
- **Share** — copy a link that opens the map on a specific lot.

## Quick start

```bash
npm install
npm run dev        # Vite dev server
npm run build      # production build
npm run preview    # serve the build
```

On a phone: open the app, tap 📍 for your location, tap ✨ for quick actions, and use 🔗 in a lot's details to share it.

### Optional: sync server

The app works fully on its own. To sync lots to a database, run Postgres and the small API in `server/`:

```bash
docker compose up -d          # Postgres 16, schema loaded from src/db/schema.sql
cd server && npm install && npm start   # API on http://localhost:3001/api
```

## Configuration

Only the sync server reads environment variables; each has a local-dev default.

- `PORT` — API port (default 3001)
- `PGHOST` — Postgres host
- `PGPORT` — Postgres port
- `PGUSER` — Postgres user
- `PGPASSWORD` — Postgres password
- `PGDATABASE` — Postgres database name

## Keyboard shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Z` / `Cmd+Z` | Undo |
| `Ctrl+Shift+Z` / `Ctrl+Y` | Redo |
| While drawing: `Ctrl+Z` | Remove last vertex |

## How it works

```
Leaflet map (src/map) ──▶ lot tools (src/lots) ──▶ IndexedDB (src/db)
        │                                              │
   tile cache ── offline                     optional sync ──▶ server/ (Express) ──▶ Postgres
```

The repo also holds an earlier Chrome extension version (`manifest.json`, `content/`, `popup/`) that draws lots directly on Google Maps.

## Docs

- [docs/README.md](docs/README.md) — documentation index
- [Getting started](docs/getting-started.md) · [Features](docs/features.md) · [Offline guide](docs/offline-guide.md)
- [Share code format](docs/SHARE_CODE.md) · [Architecture](docs/architecture.md) · [API reference](docs/api-reference.md)

## License

MIT
