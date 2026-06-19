---
name: fortune-daily-snapshot
description: Daily 08:05 fortune snapshot powering the green/red Daily Δ line on the Notion overview
---

Take the daily fortune snapshot for the user's Notion Finance Tracker (runs after the morning price updaters; powers the "Daily variation" green/red line).

COMPUTE total fortune from raw data only (formula values are not readable via API):
1. Assets total: data source 34609dd8-8306-8291-af8f-07c57f9e40dd — sum over all rows of "Price (per unit)" × "Quantity".
2. Wallets total: data source 06609dd8-8306-8392-900f-874c6a951b86 — per wallet: "Initial balance" + Amounts of linked "🟩 Income" Transactions − "🟥 Expense" Transactions (data source 53609dd8-8306-82d9-a313-87551d9bd9bf) + Transfers in − Transfers out (data source 06e09dd8-8306-8209-97a9-0759ed56ee93, by "To"/"From"). No linked rows → just Initial balance. Sum all wallets.
3. Debts total: data source 58509dd8-8306-830c-8ce8-876498d0444b — sum of ("Total value" − "Paid off" + "Final payment", treating empty fields as 0) over all rows.
4. fortune = wallets + assets − debts, rounded to 2 decimals.

WRITE: update page 84909dd8-8306-8224-b007-016631cde8b0 ("System overview", data source 5e209dd8-8306-826a-bb5a-07ef6281a0de): set number property "Fortune yesterday" = fortune. Touch nothing else. Report one line: the value written.
