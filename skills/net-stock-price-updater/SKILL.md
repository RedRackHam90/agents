---
name: net-stock-price-updater
description: Update Cloudflare (NET) stock price in CHF in the Notion Finance Tracker every 24h
---

Update the Cloudflare (NET) stock price, converted to CHF, in the user's Notion Finance Tracker.

STEPS:
1. Get the latest Cloudflare stock price in USD (ticker NET, NYSE) via WEB SEARCH (query e.g. "Cloudflare NET stock price"). Take the most recent quoted price from a reputable financial source in the results (Google Finance, Yahoo Finance, CNBC, MarketWatch). NOTE: direct quote APIs (CBOE cdn, stooq, Yahoo endpoints) return stale or empty data from this environment, so web search is the PRIMARY and authoritative source here.
2. Get the USD→CHF rate from https://api.frankfurter.app/latest?from=USD&to=CHF (JSON field rates.CHF).
3. Compute price_chf = price_usd × rate, rounded to 2 decimals.
4. In the Notion Assets data source (ID: 34609dd8-8306-8291-af8f-07c57f9e40dd), set the "Price (per unit)" number property to price_chf on the page 37609dd8-8306-8070-a02a-e5640f12b62d ("Morgan Stanley - Cloudflare Stocks"). Also update any other Assets row whose "Ticker" text = "NET".
5. Do not change Quantity or any other field. Report one line: NET price in USD, the FX rate, the CHF value written.
