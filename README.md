# Shrimpy Swims

A simple, mobile-friendly personal swim progress tracker for a friend — open to anyone who wants to use it or contribute.

Log each swim and watch cumulative distance move along fun real-world routes (like the English Channel or Loch Ness), with milestone celebrations along the way.

## Screenshots

<img width="415" height="856" alt="image" src="https://github.com/user-attachments/assets/af8cdacd-e22b-44ea-a4a7-f3bb9ec3cc34" />
<img width="435" height="870" alt="Screenshot 2026-06-16 141914" src="https://github.com/user-attachments/assets/4d002f8d-8543-4c94-a202-53b6eb7cd072" />

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
- SVG route map — your 🦐 moves along an illustrated path as you swim
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
Swim-Progression-App/
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

## Live demo

[https://lanthanum89.github.io/Swim-Progression-App/](https://lanthanum89.github.io/Swim-Progression-App/)

Install it as a PWA: open the link on your phone, tap the browser menu, and choose **Add to Home Screen**.

## Deploy your own copy

### Fork and deploy with GitHub Pages (recommended)

1. Click **Fork** at the top of this repository.
2. In your fork, go to **Settings → Pages**.
3. Under Source, choose **Deploy from a branch** → `main` / `/ (root)` → Save.
4. Your app will be live at `https://<your-username>.github.io/Swim-Progression-App/` within a minute.

All data is stored locally in the browser — each person who deploys their own fork gets their own private data.

### Run locally

1. Clone or download the repository.
2. Open `index.html` directly in your browser.

No install, no build step, no server required.

### Netlify (drag and drop)

1. Go to <https://app.netlify.com/drop>
2. Drag the project folder onto the page.

## Data Storage

Data is stored in browser `localStorage` under these keys:

- `swim_sessions_v2`
- `swim_active_route_v2`
- `swim_custom_routes_v2`
- `swim_pool_len`
- `swim_goal_date_v2`
- `swim_theme`

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

- Mobile-first (optimised for small screens)
- Simple flow for non-technical use
- Tap targets sized for touch
- Uses toast messages for user feedback

## Contributing

Contributions are welcome. Open an issue or pull request on GitHub.

## Notes for Maintainers

- Keep this as a single-file app unless requirements change.
- Prefer preserving existing storage key names to avoid breaking saved data.
- If cross-device sync is needed later, Supabase is the planned backend path.

## License

MIT License — see [LICENSE](LICENSE) for details.
