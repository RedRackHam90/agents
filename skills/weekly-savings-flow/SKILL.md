---
name: weekly-savings-flow
description: Weekly check of net savings movements in the Notion Finance Tracker (green/yellow/red dot)
---

Weekly savings-flow check for the user's Notion Finance Tracker. Compute the net money movement over the past 7 days and set a colored dot.

DATA:
- Transactions data source ID: 53609dd8-8306-82d9-a313-87551d9bd9bf — rows have "Type" ("🟥 Expense" or "🟩 Income"), "Amount" (number, CHF), and "Date & time".
- Transfers data source ID: 06e09dd8-8306-8209-97a9-0759ed56ee93 — internal moves between own wallets; ignore these (they net to zero).
- Tracker row to update: page 37709dd8-8306-814b-b1af-c73e16969491 ("📈 Weekly savings flow") in data source cb33cc7a-4cf0-4b26-ac48-0d2149349f8c.

STEPS:
1. Query/fetch the Transactions data source and collect all rows whose "Date & time" falls within the last 7 days (today inclusive).
2. net = sum(Amount of 🟩 Income rows) − sum(Amount of 🟥 Expense rows).
3. Dot: net > +50 → "🟢"; between −50 and +50 (or no transactions) → "🟡"; net < −50 → "🔴".
4. Update the tracker row: "Status" = the dot, "Detail" = e.g. "CHF +1'250 net over the last 7 days (income 3'000 / spent 1'750)" (use a − sign for negative), "date:Last checked:start" = today's date (YYYY-MM-DD).
5. Touch nothing else. Report one line with the dot and the net amount.
