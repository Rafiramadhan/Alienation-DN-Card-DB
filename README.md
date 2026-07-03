# Alienation DN Card DB

A single-page web app for browsing and filtering **Dragon Nest** monster cards — the stats
each card grants across all five rarity tiers (Magic → Rare → Epic → Unique → Legend),
plus card-pack rarity odds and the card-mastery table.

The data is sourced from the community "DN Card DB" Google Sheet and **baked into
`index.html`**, so the app is fully self-contained: no server, no database, no internet
required at runtime. Just open the file.

## Features

- **All cards** view (default) — every card and stat line in one searchable table.
- **Stat filter** — pick any of the 20 stats to see which cards give it, ranked by value.
- **Nest filter** and **card-name search**.
- **Sortable columns** — click any header; click a rarity to sort by that tier.
- **Click a card** to expand all of its stats at once.
- **Odds & Mastery** tab — pack draw rates, the Lv.40 box table, and the mastery-level table.

## Project layout

| Path                | What it is                                                        |
|---------------------|------------------------------------------------------------------|
| `index.html`        | The built app (data embedded). **This is what gets deployed.**    |
| `database.csv`      | Raw export of the Google Sheet's `Database` tab (the data source).|
| `src/template.html` | The app markup/JS with a `__DATA__` placeholder for the card data.|
| `build.js`          | Parses `database.csv` and injects it into the template.           |

## Updating the data

```bash
# Re-download the latest sheet and rebuild index.html:
node build.js --fetch

# Or rebuild from the local database.csv without downloading:
node build.js
```

Then commit the updated `index.html` (and `database.csv` if you fetched).

## Deploying (GitHub Pages)

1. Push this repo to GitHub.
2. **Settings → Pages → Source: `main` / root → Save.**
3. The site goes live at `https://<username>.github.io/Alienation-DN-Card-DB/`.

Because everything lives in `index.html`, any static host works (Cloudflare Pages,
Netlify, etc.) — just serve that one file.
