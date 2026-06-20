---
name: habit-tracker-daily-refresh
description: '[Disabled — habit tracker moved to self-rolling HTML dashboard (tracker worker); Notion DB retired]'
---

You maintain a Notion habit tracker. Use the Notion connector/MCP tools.

FIXED IDs:
- Habit Log data source: 59e3a5d8-e676-4cb9-9dfc-b767336ddd76
- "Today — tick here" view (on the main page): 37509dd8-8306-8193-8f50-000c1f3d4a73
- Per-habit progress data source: 17b01507-50e3-40be-8b30-ee09b21b71da

The 14 habits — each line is: Order = "Habit name" -> SUMMARY_PAGE_ID (the matching row in the Per-habit progress database):
1 = "Sleep by 11 ⏰"            -> 37509dd8-8306-8124-9c5a-f1c7a0441da9
2 = "Wake up at 7 ⏰"           -> 37509dd8-8306-81ec-9f4f-fb125dc682b7
3 = "No scrolling at night 📵"  -> 37509dd8-8306-817e-9810-f6f8e3c2b93e
4 = "Gym 🏋️"                    -> 37509dd8-8306-817e-b9ce-d4f17a532aa2
5 = "7K steps 👣"               -> 37509dd8-8306-816e-ad1e-e60ca05b3fef
6 = "Morning cold shower 🚿"    -> 37509dd8-8306-8176-8b60-da955af531c9
7 = "20 pages read 📖"          -> 37509dd8-8306-8130-b10b-ea01c680dadd
8 = "Daily prayer & Bible ✞"    -> 37509dd8-8306-810d-9604-d8d7a43e0c13
9 = "No alcohol 🍷"             -> 37509dd8-8306-8125-87c3-e76b833b39a8
10 = "No fast food 🍔"          -> 37509dd8-8306-8120-8ea8-ffed0d08a0f7
11 = "No porn 🚫"               -> 37509dd8-8306-8190-b21f-feaad46f7366
12 = "Call loved ones ❤️"       -> 37509dd8-8306-81a7-96ef-e7aad577422e
13 = "No waste of money 💸"     -> 37509dd8-8306-8101-843a-fa9fd57a44bc
14 = "Honor your word 🤝"       -> 37509dd8-8306-815c-9f75-c76c72cf7ab4

STEPS:
1. Determine today's date in YYYY-MM-DD (local time).
2. Search the Habit Log data source for rows whose Date = today. If 14+ rows already exist for today, skip to step 4.
3. Otherwise create one page per habit in the Habit Log data source (parent = that data source). For each habit set: "Habit" = the habit name, "Order" = its number, "date:Date:start" = today's date, leave "Done" unchecked, and set the relation "Habit ref" to the matching SUMMARY_PAGE_ID above (this keeps the per-habit % live). Never modify previous days' rows — their ticks are the saved history.
4. Update the "Today — tick here" view (ID above) filter to today: use the view-update tool with configure: CLEAR FILTER; FILTER "Date" = "<today YYYY-MM-DD>"; SORT BY "Order" ASC.

Never create duplicate rows. Keep all history intact. Report a one-line summary.
