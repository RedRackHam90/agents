---
name: schwab-portfolio-updater
description: Revalue the Schwab portfolio (18 US positions) in CHF in the Notion Finance Tracker daily
---

Revalue the user's Charles Schwab portfolio and update Notion.

HOLDINGS (ticker = quantity):
AAPL=99, AMD=20, AMZN=35, ARM=9, BA=10, GOOGL=35, LMT=25, META=22, MRVL=14, MSFT=45, NOC=3, NVDA=92.0476, PLTR=35, RTX=40, SNDK=9, TSLA=70, WDC=4, SCHX=370

STEPS:
1. For each of the 18 tickers, get the latest share price in USD via WEB SEARCH (query e.g. "<TICKER> stock price"). Take the most recent quoted price from a reputable financial source (Google Finance, Yahoo Finance, CNBC, MarketWatch). You may group a few tickers in one search to be efficient, but confirm each ticker's own current price. NOTE: direct quote APIs (CBOE cdn, stooq, Yahoo endpoints) return stale or empty data from this environment, so web search is the PRIMARY and authoritative source here.
2. Compute total_usd = sum of quantity × price across all 18 positions.
3. Fetch the USD→CHF rate from https://api.frankfurter.app/latest?from=USD&to=CHF (field rates.CHF).
4. Compute total_chf = total_usd × rate, rounded to 2 decimals.
5. In the Notion Assets data source (ID: 34609dd8-8306-8291-af8f-07c57f9e40dd), update page 2d409dd8-8306-835c-b890-81e3411daaa8 ("Charles Schwab - Stocks"): set the number property "Price (per unit)" = total_chf. Do NOT change "Quantity" (it must stay 1) or any other field.
6. Report one line: total USD, FX rate, CHF written, and note that prices came from web search.
