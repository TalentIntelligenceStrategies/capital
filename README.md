# TIS Capital & IP

The deployable landing page for **TIS Capital** (泰然資本) — the capital & IP arm of Talent Intelligence Strategies (泰然策略解密). A single static page served on its own subdomain, **[capital.tisglobalinc.com](https://capital.tisglobalinc.com/)**.

## What this repo is

One self-contained page, [`index.html`](index.html). It shares the marketing site's chrome (top nav, footer, theme toggle, language switcher, hero globe) and visual language, but lives at its own subdomain rather than under `tisglobalinc.com/capital/`.

## Shared assets — loaded from the main domain

To avoid duplicating the design system, this page **references the shared CSS, JS, fonts, and logos absolutely from the main site**:

- `https://tisglobalinc.com/assets/styles.css`
- `https://tisglobalinc.com/assets/site.js`
- `https://tisglobalinc.com/designs/assets/fonts/…` and `…/logos/…`

GitHub Pages serves `Access-Control-Allow-Origin: *`, so these load cross-origin without issue. **Consequence:** changes to the shared chrome (styles, JS, fonts) are authored in the [`website`](https://github.com/TalentIntelligenceStrategies/website) repo and propagate here automatically — there is nothing to re-sync. All cross-page nav/footer links point absolutely at `https://tisglobalinc.com/…`.

## Source of truth

The page content and styling derive from the private TIS brand monorepo (tokens, primitives, components, identity) and the marketing `website` repo (shared chrome). This repo ships only the rendered Capital page + its subdomain config. Don't author design changes here — edit upstream in the brand monorepo / `website`, then regenerate.

## Local preview

```
python3 -m http.server 8000
```

Then open [http://localhost:8000/](http://localhost:8000/). Shared assets resolve from the live `tisglobalinc.com` (absolute URLs), so styling loads as long as you're online.

## Deploy

Hosted on **GitHub Pages from the `main` branch**, served live at **[capital.tisglobalinc.com](https://capital.tisglobalinc.com/)**. The custom domain is set via the [`CNAME`](CNAME) file + a DNS `CNAME` record (`capital` → `talentintelligencestrategies.github.io`) at Squarespace. HTTPS is active.

Deploy flow: commit + push to `main` → GitHub Pages auto-rebuilds (~30s) → live.
