---
name: weekly-trainings-archive
description: Move past trainings from Notion Trainings DB to Archived trainings every Sunday at 23:00
---

Archive past trainings in the user's Notion "Health Tracker OS" workspace.

Steps:
1. Using the Notion MCP connector, search the Trainings data source (collection://ab109dd8-8306-8209-9a67-8759b56c6d42, part of database 40609dd88306823d80a6813db162b7b9, "View of Trainings and WHOOP Workouts") for all training pages. Use notion-search with data_source_url, then notion-fetch each result to read its "Date & time" property.
2. Exclude the database's default page template "New training" (page 3a309dd8-8306-83fa-aa78-01ee116c9da2) — never move it.
3. Since this runs Sunday 23:00 (end of week, weeks start Monday), archive every training whose "Date & time" start is on or before today (the current week is over). Trainings dated next week or later stay.
4. Move the matching pages with notion-move-pages to the "Archived trainings" data source: data_source_id ac32ef4c-6d59-4acd-a793-4e59cbbe4d3b (database https://app.notion.com/p/e155f2882b1b4a4ba4444d7f1f73a38c).
5. If no trainings qualify, do nothing.

Output: a one-line summary of how many trainings were archived (with their names), or "nothing to archive".
