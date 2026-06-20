---
name: monthly-finance-report
description: '1st of month 08:30 — one-message summary: fortune, spending vs budgets, savings flow, recurring costs'
---

Send the user their monthly finance report from the Notion Finance Tracker. Covers the month that just ENDED. Send it as a chat message (use the send_user_message tool if available; otherwise final report). Keep it ~10 lines, CHF with thousands separators (e.g. CHF 236'475.93).

DATA SOURCES:
- Assets: 34609dd8-8306-8291-af8f-07c57f9e40dd (Price (per unit) × Quantity per row)
- Wallets: 06609dd8-8306-8392-900f-874c6a951b86 (Initial balance + linked transactions/transfers as in other tasks)
- Debts: 58509dd8-8306-830c-8ce8-876498d0444b (Total value − Paid off + Final payment, empty = 0)
- Transactions: 53609dd8-8306-82d9-a313-87551d9bd9bf (Type 🟩 Income / 🟥 Expense, Amount, Date & time, Budgets relation)
- Month budgets: 36309dd8-8306-831b-8219-07e039a6e913 (Name, Monthly Limit)
- Subscriptions: 03109dd8-8306-8340-8838-07041108a319 (Cost, Billing cycle — monthly total = monthly costs + yearly/12)
- Fixed Costs: 1bf75f64-f136-4d5e-b5f0-ce0b444967b9 (Monthly cost)
- Summary row: page 84909dd8-8306-8224-b007-016631cde8b0 — "Fortune yesterday" number.

REPORT CONTENT (for last month):
1. 💰 Current total fortune (wallets + assets − debts, computed from raw data) and, if available, the change vs the "Fortune yesterday" value — note it's an approximate daily reference.
2. 📊 Last month's flows: total income, total expenses, net (from Transactions dated last month).
3. 🧾 Spending vs budgets: for each Month budget, the sum of last-month expenses linked to it vs its Monthly Limit (flag any overruns with ⚠️).
4. 🔄 Recurring load: subscriptions/month total + fixed costs/month total.
5. One short closing line, factual not preachy.
Never modify any Notion data in this task.
