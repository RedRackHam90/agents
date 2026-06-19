---
name: fixed-costs-due-reminder
description: Daily 09:00 check — ping the user when a fixed cost is due within 2 days or overdue
---

Check the user's Notion Fixed Costs for upcoming due payments: sync the calendar dates, and remind ONLY if something needs attention.

DATA: Fixed Costs data source ID 1bf75f64-f136-4d5e-b5f0-ce0b444967b9 — rows have "Name", "Monthly cost" (CHF), "Last paid" (date), and "Due date" (date).

STEPS:
1. For each row, compute due = "Last paid" + 1 month (empty "Last paid" counts as overdue today).
2. SYNC: if a row's "Due date" differs from the computed due, update it: set "date:Due date:start" = computed due (YYYY-MM-DD). This keeps the "Payment calendar" view accurate.
3. Collect every cost whose due date is today, within the next 2 days, or already past.
4. If that list is NOT empty: send the user a short chat message (use the send_user_message tool if available; otherwise final report) like: "💸 Fixed costs due: Rent — CHF 3'170 (due Jun 30) · Electricity — CHF 50 (overdue)". 
5. If nothing is due or near-due: stay silent (report "nothing due").
Only ever modify the "Due date" property — nothing else.
