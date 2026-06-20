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
  index.html      ← the entire app
  manifest.json   ← PWA manifest
  sw.js           ← service worker (network-first, cache fallback)
  CLAUDE.md       ← this file
  PLAN.md         ← feature roadmap
  screenshots/    ← dark-mode.jpg, light-mode.jpg
```

## localStorage schema

All keys are versioned (`_v2`) to avoid collisions with any previous prototype.

| Key | Type | Contents |
|-----|------|----------|
| `swim_sessions_v2` | JSON array | All logged swim sessions |
| `swim_active_route_v2` | string | ID of the currently selected route |
| `swim_custom_routes_v2` | JSON array | User-created routes |
| `swim_pool_len` | string (number) | Pool length in metres (default 25) |
| `swim_goal_date_v2` | string | ISO date string for target completion date |
| `swim_theme` | string | `"dark"` or absent (light default) |

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
PRESETS           — array of 7 built-in routes with milestones (inc. The Nyad)
K                 — storage key constants
getSessions()     — returns all sessions from localStorage
routeSessions()   — sessions filtered to one route
routeTotal()      — total km swum on a route
getActiveRoute()  — the currently selected route object
getGoalDate()     — returns ISO date string for target completion date
toKm()            — converts km / m / lengths to km
fmtKm()           — formats km as "1.5 km" or "500 m"
goTo(name)          — navigate between panels (home/log/history/routes/achievements)
renderHome()        — re-renders the progress/milestone view
renderHistory()     — renders session history with inline edit support
renderRoutes()      — renders route picker with completed-route styling
renderAchievements()— renders dedicated achievements screen with badge cards
submitLog()         — saves a new swim session
editSession(id)     — toggles inline edit form on a history session
saveEditSession()   — saves edited session back to localStorage
shareProgress()     — triggers Web Share API with progress message
thisWeekCount()     — count of sessions in last 7 days
calcStreak()        — consecutive weeks with at least one swim
isoWeekKey()        — returns numeric ISO week key for a date string
setGoalDate()       — saves target completion date to localStorage
exportData()        — downloads a JSON backup file
importData()        — restores from a JSON backup file
BADGE_DEFS          — array of 7 badge definitions with check functions
getBadges()         — evaluates all badges against current data (single-pass)
esc(str)            — escapes HTML for safe innerHTML usage (XSS prevention)
showCompletionModal()— accessible route completion celebration dialog
launchConfetti()    — spawns confetti pieces inside #app container
buildRouteMap()     — generates SVG route map with milestone dots
initRouteMap()      — positions shrimp and animates milestone dots
```

## How to test

Open `index.html` directly in a browser (no server needed). On mobile, host it first (see deployment).

## How to deploy

**GitHub Pages:** Push to a repo → Settings → Pages → deploy from main branch root.  
**Netlify:** Drag `index.html` into the Netlify drop zone at netlify.com/drop.

## Navigation

5-tab bottom nav: Home, History, [+ FAB], Routes, Awards.
The Log button is a raised floating action button (gradient circle, plus icon) in the centre — no label text.
Panels: `panel-home`, `panel-log`, `panel-history`, `panel-routes`, `panel-achievements`.

## Service worker

`sw.js` uses a **network-first** strategy with cache fallback for offline.
Bump `VERSION` in `sw.js` on every deploy so returning users get the latest code.
Current version: `swim-v22`.

## Conventions

- No comments except where the WHY is non-obvious.
- All CSS uses CSS custom properties defined in `:root`.
- Mobile-first: assume a ~375px wide screen. Max-width container is 480px.
- Tap targets are at least 44px tall.
- No `alert()` — use `showToast()` for all user feedback.
- Don't split into multiple files. Single-file is a hard constraint.
- `confirm()` is acceptable for destructive actions (delete swim, delete route).
- Use `esc()` for any user-provided text inserted via innerHTML (XSS prevention).
- Confetti must stay inside `#app` (`overflow: hidden`) to avoid nav stutter.
- Nav uses `will-change: transform` for compositor-layer promotion.

## If adding Supabase later

A Supabase schema (routes, sessions, user_routes tables with RLS) was built during a prior iteration and is confirmed working. If cross-device sync becomes important, Supabase is the preferred backend — add the `@supabase/supabase-js` CDN script and replace the localStorage read/write helpers. The existing data model maps directly to the Supabase schema.
