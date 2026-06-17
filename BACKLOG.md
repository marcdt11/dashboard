# Poker Dashboard — Backlog

---

### Completed
- [x] Google Sheets CSV data integration with CORS proxy fallback chain
- [x] Password-gated access (sessionStorage)
- [x] KPI stat cards (profit, hourly rate, sessions, win rate, avg hours, best/worst)
- [x] Cumulative profit chart with hourly rate toggle (Chart.js)
- [x] Multiselect filter dropdowns (location, stakes, game type) with select all/none
- [x] Filters show only options available given other active filters
- [x] Date range filter
- [x] Paginated session table (25 rows)
- [x] Responsive dark theme layout
- [x] Fallback CORS proxies for reliable data fetching
- [x] Moved to its own repo + domain (dashboard.marctorrence.com), isolated from the public poker site
- [x] Fixed "All proxies failed" data-load error — fetch the published sheet directly (it sends `Access-Control-Allow-Origin: *`); proxies demoted to fallback

### Features (Future)
_(none planned)_

### Bugs
_(none known)_

### Tech Debt
- Password hardcoded in source — fine for now, but not real auth (subdomain isolation only; page is still publicly reachable)
- CORS proxy fallback is degraded (all three currently 4xx/timeout) — direct fetch is the real path now; if Google ever drops CORS headers, data loading breaks
