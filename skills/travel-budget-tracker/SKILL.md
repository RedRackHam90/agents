---
name: travel-budget-tracker
description: 'Weekly: sync the 10K travel budget goal with the Revolut Main balance and log history for the chart'
---

Weekly travel-budget sync in the user's Notion Finance Tracker. The travel fund reference is the "Revolut Main" wallet; the goal is CHF 10'000.

FIXED IDs:
- Revolut Main wallet page: 1ab09dd8-8306-82b4-a148-0182630d421f (Wallets data source 06609dd8-8306-8392-900f-874c6a951b86) — read its raw "Initial balance" number.
- Transactions data source: 53609dd8-8306-82d9-a313-87551d9bd9bf — rows have "Wallet" (relation), "Type" ("🟥 Expense"/"🟩 Income"), "Amount".
- Transfers data source: 06e09dd8-8306-8209-97a9-0759ed56ee93 — rows have "From"/"To" (wallet relations) and "Amount".
- Goal row "✈️ Travel budget": page 37709dd8-8306-81c0-b2ba-dc33270c54df (Goals data source 60b09dd8-8306-828e-9251-871243433eeb) — update its "Current value".
- History data source: b38e20bc-6d47-485e-a012-6d0a2a753e59 (Travel fund history) — append one row per run.

STEPS:
1. Compute the current Revolut Main balance:
   balance = Initial balance
   + sum of Amount for Transactions where Wallet = Revolut Main and Type = "🟩 Income"
   − sum of Amount for Transactions where Wallet = Revolut Main and Type = "🟥 Expense"
   + sum of Amount for Transfers where To = Revolut Main
   − sum of Amount for Transfers where From = Revolut Main.
   (If there are no linked transactions/transfers, balance = Initial balance.)
2. Update the goal row: "Current value" = balance (rounded to 2 decimals). Do not touch "Target value".
3. pct = balance / 10000. Band: pct < 0.25 → "<25%"; 0.25–0.5 → "25-50%"; 0.5–0.75 → "50-75%"; ≥ 0.75 → "75%+".
4. Append a new row to Travel fund history: "Week" = e.g. "W24 ’26" (ISO week + year), "date:Date:start" = today (YYYY-MM-DD), "Balance" = balance, "Band" = the band.
5. Change nothing else. Report one line: balance, % of 10K, band.
