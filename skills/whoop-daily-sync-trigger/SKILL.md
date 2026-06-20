---
name: whoop-daily-sync-trigger
description: Daily 10:00 — trigger the WHOOP→Notion Worker sync and roll the 'Last night' sleep card filter forward
---

Keep Loris's WHOOP -> Notion sleep/recovery/workout data fresh in the "Health Tracker OS" Notion page, and keep the "Last night" sleep card pointing at the latest night.

## Background (how the pipeline works)
- A Cloudflare Worker named `whoop-notion-sync` (account: loris-impinna) syncs WHOOP -> Notion.
  Base URL: https://whoop-notion-sync.loris-impinna.workers.dev
- Endpoints:
  - `/sync?days=N`  -> forces a pull of the last N days of WHOOP cycles, sleep, recovery, workouts and upserts them into Notion. Returns JSON {started, days, daily, workouts, errors[], finished}.
  - `/`             -> status page; shows "WHOOP authorized: yes/no" and the last sync log.
  - `/auth`         -> re-authorize WHOOP OAuth if the token ever dies.
  - `/webhook`      -> WHOOP pushes here in real time, but it has proven unreliable, which is why this daily task exists as the dependable trigger.
- Notion targets:
  - WHOOP Daily data source: collection://25d4c6e8-423d-47b4-b11b-ccc41b9092ac (sleep, recovery, HRV, strain, etc.). WHOOP labels each row by the cycle START date = the evening you went to bed, so "last night" lives in the row dated YESTERDAY.
  - WHOOP Workouts data source: collection://63036932-6bbc-48c3-a958-f15b54515b29
  - "Last night" gallery view id: 37809dd8-8306-8187-b3e7-000cc9443d2b

## Step 1 - Trigger the daily sync
web_fetch: https://whoop-notion-sync.loris-impinna.workers.dev/sync?days=3
- If the JSON "errors" array is non-empty, report the errors to the user.
- If the request fails or the status page shows "WHOOP authorized: no", tell the user to re-authorize at https://whoop-notion-sync.loris-impinna.workers.dev/auth and stop.

## Step 2 - Detect and backfill gaps
Query the WHOOP Daily data source (notion-search with data_source_url collection://25d4c6e8-423d-47b4-b11b-ccc41b9092ac) for the most recent dates. If there is any missing day between the newest row and today (a gap, e.g. the Worker was idle for a stretch), re-run the sync with a wider window to backfill: web_fetch https://whoop-notion-sync.loris-impinna.workers.dev/sync?days=N where N covers the gap (max 60). Confirm the missing dates now exist.

## Step 3 - Roll the "Last night" card filter forward
The "Last night" view filters by Day on-or-after a FIXED date because the Notion API cannot store a relative date. Update it to show only the most recent night:
notion-update-view with view_id "37809dd8-8306-8187-b3e7-000cc9443d2b" and
configure: CLEAR FILTER; FILTER "Day" >= "YESTERDAY"; SORT BY "Day" DESC
where YESTERDAY = yesterday's date in YYYY-MM-DD (compute from today; last night's row is dated yesterday because WHOOP dates by cycle start).

## Output
One short line: dates synced + that the card was rolled to last night. Only elaborate if there were errors or a backfill was needed.
