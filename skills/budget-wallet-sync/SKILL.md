---
name: budget-wallet-sync
description: 'Daily: auto-assign each wallet''s expenses to the Month budget pointing at that wallet'
---

Sync wallet spending into Month budgets in the user's Notion Finance Tracker.

DATA SOURCES:
- Month budgets: 36309dd8-8306-831b-8219-07e039a6e913 — rows have "Wallet" (relation to a wallet) and "Transactions" (relation to transactions; the "Spent" rollup sums these).
- Transactions: 53609dd8-8306-82d9-a313-87551d9bd9bf — rows have "Wallet" (relation), "Budgets" (relation, max 1), "Type" ("🟥 Expense"/"🟩 Income"), "Amount", "Date & time".

STEPS:
1. List the Month budgets rows. For each budget that has a "Wallet" set:
2. Find Transactions where: Wallet = that budget's wallet, Type = "🟥 Expense", "Date & time" is in the CURRENT calendar month, and "Budgets" is EMPTY (never reassign a transaction that already belongs to a budget — manual assignments always win).
3. For each such transaction, set its "Budgets" relation to that budget's page URL.
4. If two budgets point at the same wallet, assign to the first one and mention the conflict in the report.
5. Touch nothing else (no amounts, no dates). The budget's Spent/Progress update automatically through the existing rollup. Report one line per budget: how many transactions were newly assigned.
