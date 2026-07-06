# Lehi 41st Ward — Chapel Cleaning Manager

A mobile-first web app for managing the July–October meetinghouse cleaning rotation:
monthly group assignments, family check-in, the standard cleaning checklist, and a
shared supply inventory.

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire app (HTML, CSS, and JavaScript in one file) |
| `manifest.json` | PWA manifest so the app can be installed on phones |
| `sw.js` | Service worker — makes the app work offline once installed |
| `icon-192.png`, `icon-512.png` | App icons |

## How to use it

- **Month rail (top):** tap July, August, September, or October to switch the whole app
  to that month's group. The amber dot marks the current month.
- **Home:** progress ring, family count, supply alerts, and next month's group.
- **Checklist:** tap an area (Chapel, Bathrooms, Gym…) to expand its tasks and check
  them off. "Reset month" clears everything for a fresh cleaning day.
- **Families:** tap the circle to check a family in / mark them complete.
  The search box searches every group, not just the selected month. Anyone can add a
  family with the box at the bottom, or remove one with the trash icon.
- **Supplies:** adjust quantities with +/−. Anything at 2 or fewer is flagged **Low**
  automatically; the "Request replacement" checkbox flags it for whoever buys supplies.
- **Print:** the printer icon produces a clean paper checklist with empty checkboxes
  and the month's family list — handy to tape to the supply closet door.
- **Dark mode:** the moon icon cycles Auto → Dark → Light.

## Hosting (required for PWA install)

The app is a static site — any free static host works:

1. **GitHub Pages** — create a repo, upload these five files, enable Pages in Settings.
2. **Netlify / Cloudflare Pages** — drag-and-drop the folder.

Once it's live over HTTPS, open the link on a phone and choose **Add to Home Screen**
(Share menu on iPhone, browser menu on Android). It installs like an app and works
offline inside the building.

Opening `index.html` directly from a file also works for trying it out, but install
and offline mode need a hosted HTTPS URL.

## Where the data lives

Progress, check-ins, supplies, and edits are saved in each device's browser storage
(localStorage) — no account or server needed. That means **each phone keeps its own
copy**. For most wards that's fine (one person runs the checklist on cleaning day).
If you later want everyone's checkmarks to sync live across phones, the code is
structured so the `storage` object in `index.html` can be swapped for a cloud
backend like Firebase — happy to add that if you need it.

## Customizing

All data lives at the top of the `<script>` in `index.html`:

- `GROUPS` — months, group names, and family lists
- `AREAS` — the cleaning checklist areas and tasks
- `DEFAULT_SUPPLIES` — starting inventory items
- `LOW_THRESHOLD` — the count at which a supply is flagged low
