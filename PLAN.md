# Shrimpy Swims — Plan

## Current state (built ✅)

- 6 preset routes with named milestones: English Channel, Windermere, Loch Ness, North Channel, Strait of Gibraltar, River Thames
- Swim logging: km, metres, or pool lengths (25m / 50m / custom)
- Progress bar with % complete and "distance to next milestone"
- Milestone tracker (✅ reached / 🎯 next / ⭕ future)
- Celebration screen on route completion
- Session history with delete
- Custom route builder (auto-generates 25/50/75/100% milestones)
- Export backup (JSON download) and Import restore — for saving to Google Drive
- Stats row: total swims, total distance, longest swim
- Mobile-first single-file app (no backend, no auth, no build step)
- Hosted on GitHub Pages / Netlify

---

## Possible future additions

### Tier 1 — Low effort, high value

- [ ] **More preset routes** — Serpentine (0.4 km for a quick win), Cook Strait NZ, Catalina Channel, Great North Swim distances (1.5 / 5 / 10 km)
- [ ] **Weekly streak counter** — "You've swum X weeks in a row" shown on Home
- [ ] **Swipe between panels** — touch gesture navigation on mobile (left/right swipe)
- [ ] **PWA manifest** — `manifest.json` + icons so "Add to Home Screen" gives a proper app icon and splash screen (requires a second file, breaks single-file constraint slightly)

### Tier 2 — Medium effort

- [ ] **Stats page / charts** — monthly distance bar chart, personal bests, average per session. Use a lightweight canvas chart (no library needed).
- [ ] **Route completion history** — if the user finishes the English Channel and starts again, record each "crossing" with its date and number of swims
- [ ] **Share card** — a "Share my progress" button that generates a screenshot-ready card (route name, % done, total distance) using `html2canvas` or a Canvas draw
- [ ] **Notes on milestones** — user can write a note when hitting a milestone ("I did it! Legs felt like jelly but made it to Urquhart Castle")

### Tier 3 — Larger scope

- [ ] **Supabase backend** — cross-device sync. Schema already exists from prior prototype. Would replace localStorage helpers; no UI changes needed. Requires pasting two API keys.
- [ ] **Service worker / offline mode** — cache the app shell so it works without internet once loaded (requires a second JS file)
- [x] **Route map** — SVG illustrated map showing the user's 🦐 position along the route, with milestone dots and a progress stroke. Built for all 7 preset routes.

---

## Open decisions

| Question | Status |
|----------|--------|
| Where to host? GitHub Pages or Netlify | Undecided — either works |
| Should milestones for custom routes be customisable? | Not yet — auto-generated at 25/50/75/100% |
| Push notifications / reminders? | Not planned — would require service worker + permission |
| Share the app with others? | Anyone welcome to use or contribute — see README |
