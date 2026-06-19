---
name: audi-r8-amortization
description: Credit the Audi R8 financing debt each month when the fixed cost is marked paid
---

Sync the user's Audi R8 car financing in Notion. When the monthly "Audi R8 Credit" fixed cost is marked paid for a new month, increase the paid-off amount on the "R8 Financing" debt by one monthly installment.

FIXED IDs:
- Fixed cost page "Audi R8 Credit" (Fixed costs data source 1bf75f64-f136-4d5e-b5f0-ce0b444967b9): 37709dd8-8306-81f9-b88f-d3ee67ef4681 — read its "Last paid" date and "Monthly cost" number.
- Debt page "R8 Financing" (Debts data source 58509dd8-8306-830c-8ce8-876498d0444b): 3c509dd8-8306-83f0-a753-0126a7976711 — read its "Last credited" date and "Paid off" number.

STEPS:
1. Fetch both pages and read the properties above.
2. Compare year+month of "Last paid" (fixed cost) vs "Last credited" (debt).
3. ONLY IF "Last paid" is set and its year-month is STRICTLY LATER than "Last credited" (or "Last credited" is empty): update the debt page: set "Paid off" = current Paid off + Monthly cost (e.g. +940), and set "date:Last credited:start" = the Last paid date. 
4. Otherwise do nothing (this prevents double-counting — the task runs daily but must credit at most once per month).
5. Never decrease values, never modify "Total value" or any other field. Report one line: either "no new payment" or the new Paid off amount.
