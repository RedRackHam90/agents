---
name: subscription-renewal-pings
description: Daily 09:05 — ping the user when a subscription renews within 2 days; silent otherwise
---

Check the user's Notion Subscriptions for upcoming renewals and remind ONLY if something is close.

DATA: Subscriptions data source 03109dd8-8306-8340-8838-07041108a319 — rows have "Name", "Cost" (CHF), "Billing cycle" ("Monthly"/"Yearly"), "Start date".

STEPS:
1. For each subscription, compute the next renewal: starting from "Start date", advance by 1 month (Monthly) or 1 year (Yearly) repeatedly until the date is today or in the future. Empty Start date → skip the row.
2. Collect subscriptions renewing today or within the next 2 days.
3. If the list is NOT empty: send the user a short chat message (use the send_user_message tool if available; otherwise final report), e.g. "🔄 Renewing soon: DAZN — CHF 34.90 (Jun 14) · Swisscom — CHF 175 (Jun 15)".
4. If nothing renews within 2 days: stay silent (report "nothing renewing").
Never modify any Notion data in this task.
