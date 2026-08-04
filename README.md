# GCS Tour App — Oakham 2026 (England U15s)

Build: **2026-08-04a · u15s-oakham**
Database: **GCS_OAKHAM_U15_APP_DATABASE_v1.xlsx**
Dates: **Tuesday 11 – Friday 14 August 2026**

Same universal shell as the Oakham U13s build, re-pointed at the U15s tournament.

------------------------------------------------------------
## What's in this bundle
- `index.html` .................. the main app (players, supporters, staff, scorers/umpires, admin)
- `admin.html` .................. the organiser console (Import spreadsheet, then Publish)
- `netlify/functions/tour.mjs` .. the backend (itinerary, alerts, votes, batting orders)
- `start.html` .................. the public "get the app" page for parents, players and team staff
- `manifest.json`, `sw.js` ...... installable + always-fresh
- `_headers` .................... no-store cache headers
- `netlify.toml` ................ publish dir = root, functions = netlify/functions
- `favicon.png`, `favicon.svg` .. app icon

The spreadsheet is deliberately **not** in this bundle.

------------------------------------------------------------
## Version numbering

The U15s start a **new numbering series at v1**. The Oakham U13s build (app v90,
database v35) is untouched and keeps its own numbers. Build stamps restart at `a`
and advance alphabetically from here.

------------------------------------------------------------
## What changed from the U13s build

| Change | Where |
|---|---|
| Build stamp reset to `2026-08-04a · u15s-oakham` | index.html, admin.html |
| Admin console subtitle now reads **Oakham U15s 2026** (was Tobago 2026) | admin.html |
| Squad count copy: eight/seven squads → **six/five** squads | index.html, start.html |
| Day-of-week copy: Monday → **Tuesday**, Thursday → **Friday** | index.html, start.html |
| Age reference: shy 12-year-old → **14-year-old** | index.html, start.html |
| Header dates: 3–6 August → **11–14 August** | start.html |
| Countdown target: 3 Aug 14:30 → **11 Aug 2026, 14:30** | start.html |

Everything else is untouched. Team names, fixtures, schedule, packing list, FAQ, contacts
and the challenge list all come from the spreadsheet — no code changes needed for those.

------------------------------------------------------------
## Still to do before go-live

1. **Fixture grid.** The Games tab in v1 is empty (header row only). Paste the grid in,
   re-import and publish.
2. **Groups.** The Teams tab has a blank Groups column. Fill it in at the same time as the
   fixtures, or any "Group 1 1st" style bracket names in the Games tab will not resolve.
3. **Squad numbers.** The U15 squad lists did not carry them, so the Players tab has a blank
   Squad Number column. Add them if you want them showing.
4. **`manifest.json`** still describes the U13s tournament and **`start.html`** still points its
   `og:url` / `og:image` at `oakham.globalcricketseries.com`. If this goes on a new subdomain,
   those two need re-pointing. Left alone here on purpose.

------------------------------------------------------------
## No transport at Oakham

Nobody is bussed anywhere. There are no flights, coaches, minibuses or transfers at any point.
Everyone makes their own way to Oakham School and home again. To keep it that way:

- leave the **Departures** tab empty (header row only),
- leave the outbound/inbound travel rows in **Tour Details** blank,
- leave the **Return Hotel** column on the Games tab blank,
- don't add Travel-type schedule rows other than arrival and departure.

That combination — no flight numbers plus a UK **Country** value — is what puts the app into
**domestic tour mode**, which hides Flights, Airport departures, Travel money, Mobile data (eSIM),
Visas and the Online landing card, and relabels the hotel tile as **Where we stay · Map** for
players and staff. Supporters still see **Hotel · Map** for the Wisteria.

The roll-call register on the Schedule is **kept** — it is a head count, not a bus register, and
is still useful at meals and before matches.

------------------------------------------------------------
## Deploying

New site (recommended, so the U13s build stays live):
1. New GitHub repo with these files at the root, keeping `netlify/functions/` exactly as-is.
2. Netlify → Add new site → Import an existing project → pick the repo.
3. Build command: blank. Publish directory: `.` Functions: blank.
4. Deploy, then rename the site under Site configuration → Change site name.
5. Check the Netlify **Functions** tab shows `tour`.

Then open `<your-url>/admin.html`, load `GCS_OAKHAM_U15_APP_DATABASE_v1.xlsx`, and press
**Publish**. The site is empty until you publish — that's expected.

------------------------------------------------------------
## Updating later
- **Data** (schedule, fixtures, squads, More content, FAQ): edit the spreadsheet → Import in
  admin.html → Publish. No deployment.
- **Code** (index.html / admin.html): push to GitHub, Netlify redeploys. No re-import.
