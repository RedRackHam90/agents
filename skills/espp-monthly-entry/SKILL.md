---
name: espp-monthly-entry
description: On the 30th, pre-create the monthly ESPP contribution row in Notion and remind Loris to enter the amount
---

Use the Notion MCP tools (server: notion) to create one page in the "ESPP Contributions" data source, ID: ceef547c-8c41-4e86-8b32-d0eab705e9a8 (parent type data_source_id).

Properties for the new page:
- "Month": the current month and year in English, e.g. "June 2026"
- "date:Date:start": today's date as YYYY-MM-DD
- "Asset": "[\"https://app.notion.com/p/37709dd88306808aa263c6353fc426cd\"]" (this links it to the Cloudflare ESPP asset)
- Leave "Amount" empty — Loris fills it in manually.

Before creating, search the data source for an existing page with the same Month title to avoid duplicates; if it already exists, do nothing.

Then send Loris a short message: the ESPP row for this month is ready in Notion — just open it and type the amount. Include the new page's URL.
