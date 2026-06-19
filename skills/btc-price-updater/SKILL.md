---
name: btc-price-updater
description: Update Bitcoin price (CHF) in the Notion Finance Tracker Assets twice daily (09:00 & 18:00)
---

Update the live Bitcoin price (in CHF) in the user's Notion Finance Tracker.

STEPS:
1. Fetch the current BTC price in CHF from: https://api.coinbase.com/v2/prices/BTC-CHF/spot  → the price is the JSON field data.amount (a string; convert to a number, round to 2 decimals).
   - If that request fails, try https://api.coinbase.com/v2/prices/BTC-CHF/buy as a fallback.
2. In the Notion Assets data source (ID: 34609dd8-8306-8291-af8f-07c57f9e40dd), update the "Price (per unit)" number property to that value for every row whose "Ticker" text = "BTC". These are the known Bitcoin rows (update each):
   - 37609dd8-8306-8054-9c02-ef4e0197a515  (Coinbase - Bitcoin)
   - 6ff09dd8-8306-82bf-978d-0193593f618e  (Kraken - Bitcoin)
   - 37609dd8-8306-8010-a8fc-d97da3a418c7  (Revolut - Bitcoin)
   - 37609dd8-8306-8020-8db1-def7d8f53961  (Swissquote - Bitcoin)
   Also update any additional Assets row that has Ticker = "BTC" in case the user added more.
3. Do not change Quantity or any other field. Only set "Price (per unit)".
4. Report a one-line summary: the BTC/CHF price used and how many rows updated.
