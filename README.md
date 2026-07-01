# Relief Pledge Registry

A public accountability ledger tracking relief pledges made after the June 24,
2026 doublet earthquake (M7.2 → M7.5) west of Caracas, Venezuela — against
independently confirmed on-the-ground delivery.

High-profile donations (sports teams, businessmen, corporations, governments)
get headlines when announced. This page tracks each pledge through three
custody stages — **announced**, **operational / in transit**, and
**confirmed delivered** — so the gap between a headline and a delivered good
is visible, not assumed.

## What this is

- A single static HTML file: `venezuela-relief-ledger.html`
- No framework, no build step, no backend — every ledger entry is a hardcoded,
  manually sourced record in the page's own `data[]` array
- Not a fundraising page, and not affiliated with any of the organizations or
  donors it tracks

## Status

Actively maintained by hand as coverage develops. Not yet hosted publicly —
this repo exists ahead of a hosted release once the ledger and its data
pipeline are further along.

## Contributing

This is a manually curated dataset by design — entries are added one at a
time from primary or wire sources, not scraped or auto-generated, to avoid
propagating misreported figures. If you spot an error or have a source for
a status update, open an issue with a link to the primary source.
