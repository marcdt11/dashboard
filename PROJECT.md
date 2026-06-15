# Poker Dashboard — Project Overview

## What It Is
Private analytics dashboard for NLHE session tracking. Pulls session data from a
published Google Sheet CSV and renders KPIs, a cumulative-profit chart, filters,
and a paginated session table.

Formerly hosted at `poker.marctorrence.com/dashboard`; moved to its own repo +
domain so it is not discoverable from the public poker tools site.

## Architecture
- **No build tools, no frameworks.** Vanilla HTML/CSS/JS in a single `index.html`.
- **Client-side only.** No backend, no database — reads a published Google Sheet CSV.

## Folder Structure
```
/
├── PROJECT.md     # This file
├── BACKLOG.md     # Feature backlog + completed items
├── README.md      # Quick overview
├── CNAME          # Custom domain (dashboard.marctorrence.com)
└── index.html     # The dashboard app
```

## Deployment
- GitHub Pages from `main` branch, root `/` path
- Repo: `marcdt11/dashboard`
- Custom domain: `dashboard.marctorrence.com`
- DNS: `dashboard` CNAME → `marcdt11.github.io` (GoDaddy)
- No CI/CD — push to main auto-deploys

---

## Technical Details

### Data Source
- Published Google Sheet CSV fetched client-side
- CORS proxy fallback chain (allorigins → corsproxy.io → api.codetabs.com) for reliable cross-origin fetching
- Cache-busting query param appended to each request
- Fetch kicks off on script load (parallel with the password gate) rather than after submit, so data is ready by the time the user enters the password — `csvPromise` is created at module scope and awaited inside `init()`

### Authentication
- Simple password gate stored in `sessionStorage` (password hardcoded in source — not secure, just a casual gate)

### Features
- **KPI Cards** — Total profit, hourly rate, session count, win rate, avg session hours, best/worst session
- **Cumulative Profit Chart** — Chart.js line chart with toggle between cumulative profit and hourly rate views
- **Filters** — Multiselect dropdowns for location, stakes, game type + date range inputs. Dropdowns show only options available given other active filters. Select all/none controls.
- **Session Table** — Paginated (25 rows), sortable, showing date, location, game, stakes, hours, buy-in, cash-out, profit
- **Responsive** — Mobile-friendly layout; viewport `maximum-scale=1.0` prevents iOS auto-zoom on input focus (e.g. tapping the password field) which would otherwise persist after the keyboard closes; `text-size-adjust: 100%` on `body` prevents iOS Accessibility "Larger Text" from inflating text and overflowing the viewport (user pinch-zoom still works on iOS 10+)

### Design System
- Dark GitHub-style theme (`--bg-primary: #0d1117`)
- Fonts: Outfit (UI) + JetBrains Mono (numbers)
- Green/red profit coloring

## Known Issues
- **Security**: The subdomain keeps the dashboard off the public poker site, but the page itself is publicly reachable to anyone who knows the URL, and the password is hardcoded in source (not a real security measure). The underlying Google Sheet is published/public.
- **CORS proxies**: Relies on third-party CORS proxies which may go down; fallback chain mitigates but doesn't eliminate risk.
