# Relief Pledge Registry — Venezuela Earthquake Relief Ledger · Claude Code Session

## Project context
Single-file HTML tracker for public accountability of Venezuela earthquake relief
pledges (June 24, 2026 doublet quake, M7.2 → M7.5, west of Caracas).
File: `venezuela-relief-ledger.html`

Standalone civic-transparency project. Not part of ACQUATELLA Ingeniería, MirIAm BI,
Ptolemy III, or Croesus — separate purpose, separate audience.

Purpose: track publicly announced relief pledges against independently confirmed
on-the-ground delivery, in response to public concern that high-profile donations
(sports teams, businessmen, corporations) may not reach affected communities.

## Current state
V1 built in Claude Chat, not yet touched by Code. Stack:
- Pure HTML/CSS/JS — no framework, no build step, single file
- Google Fonts: IBM Plex Mono (labels/data/headers) + IBM Plex Sans (body)
- No external JS libraries — vanilla search/filter/summary calculation
- CSS custom properties for all colors
- 9 seeded ledger entries, manually curated and sourced — no scraping, no
  auto-generation

## Design system (do not break these)
Palette is dark graphite/night-toned — deliberately NOT the cream+serif or
near-black+acid-accent looks that read as AI-generated defaults:

- `--bg:#14181F` `--surface:#1E232B` `--surface-2:#262C36`
- `--ink:#E7E3D8` `--ink-dim:#9BA3AE` `--line:rgba(231,227,216,.12)`
- Status colors: `--pledged:#D98E3F` (amber) · `--transit:#6E8FB0` (steel blue) ·
  `--confirmed:#4FA88F` (teal) · `--critical:#B5493D` (brick red — casualty stats
  only, never used decoratively)

Typography: IBM Plex Mono for all data/labels/headers/stats (instrument-readout
feel); IBM Plex Sans for donor names, notes, body copy.

Signature element: the 3-stage **custody stepper** per row (Announced →
Operational/In Transit → Confirmed Delivered). This *is* the point of the tool —
never collapse it to a binary "donated / not donated" state.

Tone: sober and restrained. No glassmorphism, no gradients, no celebratory
dashboard styling. The subject is a mass-casualty disaster, not a product launch.

## Data architecture — CRITICAL
All ledger entries are hardcoded in the `data[]` array inside the `<script>` block.

Schema per entry:
```
donor, type, amountUSD (number | null), amountDisplay (string),
date (YYYY-MM-DD), status ('pledged'|'in-transit'|'confirmed'),
recipient, sourceName, url, note
```

- `amountUSD: null` is intentional and meaningful — it means the amount is
  undisclosed. Never guess or backfill a number to fill the gap.
- The stats bar (`#stats`) computes totals live from `data[]`. Never hardcode
  the summary numbers themselves.
- Every entry needs a real, checkable `url` from a primary or wire source.
  Never add a row without one.

## What to work on (priority order)
1. **Data refresh workflow** — add new entries as coverage develops (see
   "Updating the ledger" below)
2. **Status promotion** — move entries from `pledged`/`in-transit` → `confirmed`
   only when independent reporting confirms actual on-the-ground delivery or
   audited spend; the `note` field must say what evidence justified the move
3. **Spanish localization** — toggle or full es-VE translation. The audience most
   invested in this page is Spanish-speaking
4. **Hosting** — static deploy (GitHub Pages / Netlify) so it's a shareable
   public link, not a local file
5. **Optional**: a lightweight "submit a correction" contact note — keep manual
   review, no auto-publish of reader submissions

## Updating the ledger
- Add entries by hand to `data[]`, one object per pledge, always with a real
  source URL
- Do not scrape or auto-ingest headlines — misreported pledge figures get
  quietly corrected or retracted upstream, and reproducing them here without
  a check spreads the error further
- When promoting a `status` to `confirmed`, cite the specific evidence
  (independent audit, journalist on the ground, org's own disbursement report)

## Session rules
- Single HTML file only — no external JS/CSS files, no bundler, no build tooling
- Preserve the `data[]` array pattern exactly — don't refactor into fetch calls
  or a backend unless explicitly asked
- Show diffs before structural changes (layout, schema), not just before
  styling tweaks
- Never invent or round up a donation figure to fill a gap — "undisclosed"
  stays "undisclosed" until it's sourced
