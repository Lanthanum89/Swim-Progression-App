# Shrimpy Swims — Claude Code context

## What this is

A personal swim progress tracker, built for a friend — but open for anyone to use or contribute to. The user logs swims; the app visualises cumulative distance as movement along a named route (English Channel, Loch Ness, etc.). Think a fundraising progress bar but personal and ongoing.

**End user:** non-technical swimmer. UX must be simple and low-friction.  
**Maintainer:** project owner.

## Stack

- Single file: `index.html` — all HTML, CSS, and JS in one file. No build step, no dependencies, no framework.
- Storage: `localStorage` (browser). No backend, no auth.
- Hosting: GitHub Pages or Netlify (drag and drop `index.html`).

## File structure

```
Swim-Progression-App/
  index.html    ← the entire app
  CLAUDE.md     ← this file
  PLAN.md       ← feature roadmap
```

## localStorage schema

All keys are versioned (`_v2`) to avoid collisions with any previous prototype.

| Key | Type | Contents |
|-----|------|----------|
| `swim_sessions_v2` | JSON array | All logged swim sessions |
| `swim_active_route_v2` | string | ID of the currently selected route |
| `swim_custom_routes_v2` | JSON array | User-created routes |
| `swim_pool_len` | string (number) | Pool length in metres (default 25) |

### Session object
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

### Custom route object
```json
{
  "id": "custom-1718530000000",
  "name": "My Local Lake",
  "emoji": "🗺️",
  "desc": "Custom route",
  "km": 5,
  "custom": true,
  "milestones": [
    { "km": 0,    "label": "Start!" },
    { "km": 1.25, "label": "25% of the way" },
    { "km": 2.5,  "label": "Halfway!" },
    { "km": 3.75, "label": "75% done" },
    { "km": 5,    "label": "My Local Lake complete! 🎉" }
  ]
}
```

## Key JS structure (inside `index.html`)

```
PRESETS         — array of 6 built-in routes with milestones
K               — storage key constants
getSessions()   — returns all sessions from localStorage
routeSessions() — sessions filtered to one route
routeTotal()    — total km swum on a route
getActiveRoute()— the currently selected route object
toKm()          — converts km / m / lengths to km
fmtKm()         — formats km as "1.5 km" or "500 m"
goTo(name)      — navigate between panels (home/log/history/routes)
renderHome()    — re-renders the progress/milestone view
submitLog()     — saves a new swim session
exportData()    — downloads a JSON backup file
importData()    — restores from a JSON backup file
```

## How to test

Open `index.html` directly in a browser (no server needed). On mobile, host it first (see deployment).

## How to deploy

**GitHub Pages:** Push to a repo → Settings → Pages → deploy from main branch root.  
**Netlify:** Drag `index.html` into the Netlify drop zone at netlify.com/drop.

## Conventions

- No comments except where the WHY is non-obvious.
- All CSS uses CSS custom properties defined in `:root`.
- Mobile-first: assume a ~375px wide screen. Max-width container is 480px.
- Tap targets are at least 44px tall.
- No `alert()` — use `showToast()` for all user feedback.
- Don't split into multiple files. Single-file is a hard constraint.
- `confirm()` is acceptable for destructive actions (delete swim, delete route).

## If adding Supabase later

A Supabase schema (routes, sessions, user_routes tables with RLS) was built during a prior iteration and is confirmed working. If cross-device sync becomes important, Supabase is the preferred backend — add the `@supabase/supabase-js` CDN script and replace the localStorage read/write helpers. The existing data model maps directly to the Supabase schema.
