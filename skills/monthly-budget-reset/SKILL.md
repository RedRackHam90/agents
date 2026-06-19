---
name: monthly-budget-reset
description: '1st of month: detach last month''s transactions from Month budgets so they restart at 0%'
---

Monthly budget reset for the user's Notion Finance Tracker. The "Spent" rollup on each Month budget sums ALL transactions linked to it; without a reset, budgets accumulate forever. Detach old links so each budget restarts the new month at 0%.

DATA:
- Transactions data source: 53609dd8-8306-82d9-a313-87551d9bd9bf — rows have "Budgets" (relation, max 1) and "Date & time".
- Month budgets data source: 36309dd8-8306-831b-8219-07e039a6e913.

STEPS:
1. Find all Transactions whose "Budgets" relation is NOT empty AND whose "Date & time" is BEFORE the 1st of the current month.
2. For each, clear the "Budgets" relation (set it to an empty list). Do NOT delete the transaction, do NOT touch its amount, wallet, date, or anything else — only empty the Budgets relation.
3. Leave current-month transactions fully untouched.
4. Report one line: how many transactions were detached.
