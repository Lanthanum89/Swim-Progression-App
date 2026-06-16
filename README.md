# Shrimpy Swims

A simple, mobile-friendly swim progress tracker for Beth.

Log each swim and watch cumulative distance move along fun real-world routes (like the English Channel or Loch Ness), with milestone celebrations along the way.

## Highlights

- Single-file app (no build step, no framework)
- Fast local-first data storage with browser `localStorage`
- Route-based progress with milestones
- Swim logging with flexible units:
  - km
  - m
  - pool lengths
- Session history and route management
- Data backup and restore (JSON export/import)
- Works great on GitHub Pages or Netlify

## Tech Stack

- HTML, CSS, JavaScript in one file: `index.html`
- PWA support files:
  - `manifest.json`
  - `sw.js`
- No backend
- No authentication
- No dependencies

## Project Structure

```text
Beth-swim-app/
  index.html      # entire app UI + logic
  manifest.json   # PWA manifest
  sw.js           # service worker
  PLAN.md         # roadmap notes
  CLAUDE.md       # maintainer/project context
```

## Run Locally

1. Open `index.html` directly in your browser.
2. Start logging swims.

No install required.

## Deployment

### GitHub Pages

1. Push this repository to GitHub.
2. Go to repository settings.
3. Open the Pages section.
4. Deploy from the `main` branch root.

### Netlify (drag and drop)

1. Go to <https://app.netlify.com/drop>
2. Drag `index.html` (or the full project folder).

## Data Storage

Data is stored in browser `localStorage` under these keys:

- `swim_sessions_v2`
- `swim_active_route_v2`
- `swim_custom_routes_v2`
- `swim_pool_len`

### Session Shape

```json
{
  "id": "1718530000000",
  "date": "2026-06-16",
  "dist_km": 1.5,
  "unit": "km",
  "unit_val": 1.5,
  "note": "Felt great!",
  "route_id": "english-channel"
}
```

## UX/Design Notes

- Mobile-first (optimized for small screens)
- Simple flow for non-technical use
- Tap targets sized for touch
- Uses toast messages for user feedback

## Notes for Maintainers

- Keep this as a single-file app unless requirements change.
- Prefer preserving existing storage key names to avoid breaking saved data.
- If cross-device sync is needed later, Supabase is the planned backend path.

## License

No license file is currently included.
Add one if you plan to distribute or open-source this project.
