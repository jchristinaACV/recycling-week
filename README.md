# Hamburg Recycling Week

A single-page lookup for curbside recycling in the Town of Hamburg, NY. Pick your
street once and it tells you whether this is your week, when the next pickup is,
which weeks include bulk items, and when a holiday pushes collection back a day.

Live site: https://jchristinaacv.github.io/recycling-week/

## How it works

The town runs two alternating schedules, A week and B week, and assigns every
street to one of them plus a weekday. Those assignments come from the town's
printed street listing; the A/B alternation comes from the Modern Disposal
collection calendar.

Three rules drive everything:

- **A/B weeks alternate with no skips.** The app anchors on the week of Sunday
  April 5, 2026 (printed as an A week) and computes parity from there. This was
  checked against all 41 colored weeks on the 2026 calendar — no mismatches.
- **Holidays delay collection one day for the rest of that week.** Observed
  holidays are New Year's Day, Memorial Day, Independence Day, Labor Day,
  Thanksgiving and Christmas. A holiday falling on a Saturday shifts nothing,
  matching how the 2026 calendar prints July 4.
- **Bulk pickup is the second Monday of April, June, August, October and
  December**, on your normal collection day. That rule reproduces all five
  dates printed for 2026.

## Files

- `index.html` — the whole app, self-contained. No build step and no
  dependencies. Street data is inlined, so the only outside request is a
  Google Fonts stylesheet; delete that one `<link>` and it works offline.
- `streets.json` — the same street listing as standalone data, for reference
  and easier diffing. The app does not read it; corrections have to go into
  the copy inlined in `index.html` too.

## Known quirks in the source listing

- 23 roads are split into segments by cross street (Lakeview Rd, Southwestern
  Blvd, Amsdell Rd and others), so they appear more than once. The app shows
  each segment as its own choice.
- **Eckhardt Rd is listed twice** — once under B-Thursday, once under
  B-Friday — with no segment note either time to distinguish them. Both are
  preserved as printed rather than guessed at.
- The printed 2026 calendar leaves January 1 through March 21 uncolored. Those
  weeks are filled in by continuing the same alternation backwards.

Verify anything that matters against the town's own schedule.

## Hosting

Static file, so any host works. For GitHub Pages: Settings → Pages → Source
"Deploy from a branch" → `main` / `/ (root)`.
