# Poker Dashboard

Private analytics dashboard for NLHE session tracking. Pulls session data from a
published Google Sheet CSV and renders KPIs, a cumulative-profit chart, filters,
and a paginated session table.

- **Live:** https://dashboard.marctorrence.com
- **Stack:** Single self-contained `index.html` (vanilla HTML/CSS/JS), no build step.
- **Hosting:** GitHub Pages from `main` (root), custom domain via `CNAME`.

> Note: protected only by a casual client-side password gate. The subdomain keeps
> it off the public `poker.marctorrence.com` site, but the page itself is publicly
> reachable to anyone who knows the URL.
