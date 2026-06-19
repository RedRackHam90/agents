---
name: swissquote-portfolio-updater
description: Revalue the Swissquote stocks (NET/NVDA/SNDK) and gold (XAU) in CHF in the Notion Finance Tracker, twice daily (07:25 & 18:00)
---

Revalue the user's Swissquote holdings and update Notion.

STOCK HOLDINGS (ticker = quantity): NET=25, NVDA=5, SNDK=10
GOLD: 3 troy ounces (XAU)

STEPS:
1. For each stock ticker (NET, NVDA, SNDK), get the latest share price in USD via WEB SEARCH (query e.g. "<TICKER> stock price"). Take the most recent quoted price from a reputable financial source (Google Finance, Yahoo Finance, CNBC, MarketWatch). NOTE: direct quote APIs (CBOE cdn, stooq, Yahoo endpoints) return stale or empty data from this environment, so web search is the PRIMARY and authoritative source here.
2. Fetch the gold price in USD per ounce from https://api.gold-api.com/price/XAU (JSON field "price"). Fallback: web search "gold price per ounce USD".
3. Fetch the USD→CHF rate from https://api.frankfurter.app/latest?from=USD&to=CHF (field rates.CHF).
4. Compute:
   - stocks_total_chf = (25×NET + 5×NVDA + 10×SNDK) × rate, rounded to 2 decimals
   - gold_per_oz_chf = gold_usd × rate, rounded to 2 decimals
5. In the Notion Assets data source (ID: 34609dd8-8306-8291-af8f-07c57f9e40dd):
   - Update page 37709dd8-8306-8076-9df2-fe2519237ac2 ("Swissquote - Stocks"): set "Price (per unit)" = stocks_total_chf. Quantity must stay 1 — do not change it.
   - Update page 37709dd8-8306-818a-ae04-fa2fe02098c9 ("Swissquote - Gold"): set "Price (per unit)" = gold_per_oz_chf. Quantity must stay 3 — do not change it.
6. Change nothing else. Report one line: each USD price, the FX rate, and the two CHF values written.
