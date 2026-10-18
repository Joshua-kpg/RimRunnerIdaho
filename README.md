# RimRunnerIdaho

Unofficial Idaho HS boys basketball ratings. Not affiliated with the IHSAA or MaxPreps.
Status: **HELD (waiting on hosting)**. Preview: https://joshua-kpg.github.io/RimRunnerIdaho/ (GitHub Pages). No Firebase project yet
(the Google accounts are at their project quota) and Cloudflare Pages is at its project limit, so accounts, picks and follows save only in the
visitor's browser until the site's own Firebase project exists.

## Files
- `index.html` — the whole app (data embedded). `logos/` — small WebP school logos (from MaxPreps school profiles), served with the site.
- `data/results.json` — 2026-27 finals ledger written by the nightly updater.
- `firebase/` — Firestore rules and auth config for the site's future Firebase project (accounts, picks, follows).

## Teams
158 teams: the IHSAA member schools on MaxPreps with a boys varsity team, classed by the IHSAA 2026-28 Member Schools directory with the
boys basketball exceptions from the IHSAA board's appeal results (Canyon Ridge 5A, Wood River 4A, Alturas Prep 2A):
6A 20, 5A 24, 4A 19, 3A 29, 2A 35, 1A 31. Highland (Craigmont) plays as the MaxPreps Highland/Culdesac co-op. No Other (non-IHSAA)
programs met the 8-game rule. Conferences = each school's MaxPreps 2026-27 conference (26 with 2+ listed teams), with five IHSAA 2026-28
moves that MaxPreps has not posted yet (Middleton 6A SIC, Emmett 4A SRV, Marsh Valley 3A SEIC, North Star Charter 3A WIC, Canyon Ridge
5A Great Basin). IHSAA districts I-VI are postseason only and are not used as conferences.

## Season rule
IHSAA 2026-27 boys basketball First Game = Sat Nov 28, 2026 (IHSAA "2026-27 Basketball" sheet). Games involving an IHSAA school before that
date are left out (schedule build and nightly updater); games between two non-IHSAA schools are kept. State tournaments Mar 4-6, 2027.

## Nightly scores
`.github/workflows/nightly-scores.yml` runs `scripts/update_scores.py` at 06:30 and 14:00 UTC (11:30 pm / 7:00 am Mountain standard time) and
on manual dispatch. Before `SEASON_START` in index.html (the first game on the MaxPreps schedules) the script makes no requests. From then on it
reads boys basketball finals for the last 3 days from the MaxPreps Idaho scores-by-date page (team-page fallback), matches them to the schedule
by MaxPreps team id + date, records them in `data/results.json` and bakes scores and W-L records into `index.html`. The page recomputes Elo
from those finals. It commits only when data changed; GitHub Pages updates from the commit.
