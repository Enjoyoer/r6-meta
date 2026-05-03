# R6 Meta Armory

A public Rainbow Six Siege attachment meta dashboard for quickly browsing recommended loadouts by operator, weapon, optic, muzzle, grip, and underbarrel.

Live site: https://enjoyoer.github.io/r6-meta/

## What It Includes

- Dashboard stats for total loadouts, operators, weapons, and top attachments.
- Chart.js visualizations for muzzle mix and weapon category coverage.
- Search and filters for weapon type, muzzle, grip, and underbarrel.
- Sortable database table.
- Pinned loadouts and a compare board.
- Filtered CSV copy/export.
- Dark and light theme support.

## Project Structure

- `index.html` - public GitHub Pages app.
- `r6_loadouts.csv` - source data used by the app.
- `R6 Attachment Guide.pdf` - reference guide linked from the site.
- `classic.html` - previous standalone dashboard kept for compatibility.
- `archive/` - archived copies of older dashboard builds.
- `docs/` - design notes and implementation plans.
- `r6_optimization_handoff.md` - R6 performance tuning notes.
- `r6_verification_checklist.md` - tuning verification checklist.

## Data Format

`r6_loadouts.csv` uses this column order:

```csv
Category,Weapon,Operator,Optic,Muzzle,Grip,Underbarrel
```

To update the public recommendations, edit `r6_loadouts.csv` and keep the same headers. The site fetches that file at runtime.

## Local Preview

From the repository root:

```powershell
python -m http.server 4173
```

Then open:

```text
http://localhost:4173
```

Using a local server is recommended because the app loads `r6_loadouts.csv` with `fetch()`.

## Private Tools

Personal workflow tools, including the checklist page, are kept local-only under `private/`. That folder is ignored by Git and is not published to GitHub Pages.

## Deployment

The site is deployed with GitHub Pages from the `main` branch.
