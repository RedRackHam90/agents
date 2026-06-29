---
name: meal-macro-calc
description: Estimate calories and macros (protein/carbs/fat) for free-text meals logged in Loris's Notion "My Meals" database, then write them back and tick the Calculated checkbox. Use when asked to "calculate my meals", "fill in macros", "compute calories for what I ate", or to backfill un-calculated meal entries.
---

# Meal Macro Calculator

Estimate calories and macros for entries in the Notion **My Meals** log and write them back.

## Target

- Data source: `collection://c2f9c001-4196-4f90-8bb5-c22ac7b4bdbc` (My Meals)
- Properties:
  - `Meal` (title) — free-text description of what was eaten
  - `Type` (select) — Breakfast / Lunch / Dinner / Snack
  - `Date` (date)
  - `Calories`, `Protein (g)`, `Carbs (g)`, `Fat (g)` (numbers) — to fill in
  - `Calculated` (checkbox) — tick once filled

## Procedure

1. **Find un-calculated entries.** Query the data source for rows where `Calculated` is not set:
   ```sql
   SELECT url, "Meal", "Type", "date:Date:start" AS d, "Calculated" AS done
   FROM "collection://c2f9c001-4196-4f90-8bb5-c22ac7b4bdbc"
   WHERE "Calculated" != '__YES__' OR "Calculated" IS NULL
   ```
   On a `429` rate-limit, wait ~30s and retry.

2. **Estimate per entry.** Read the `Meal` text and estimate whole-meal Calories (kcal), Protein (g), Carbs (g), Fat (g) using standard nutrition values:
   - Use stated quantities where given (e.g. "150g skyr", "300g minced beef", "1 scoop whey", "100g nut mix").
   - Where no quantity is given (e.g. "bread", "pasta", "olive oil"), assume a typical single serving and keep estimates reasonable.
   - **Consistency check:** `4*Protein + 4*Carbs + 9*Fat` should be within ~5% of Calories. Adjust if wildly off.

3. **Write back & tick.** For each entry:
   ```
   notion-update-page
     page_id: <id from the entry url>
     command: update_properties
     properties: {
       "Calories": <kcal>,
       "Protein (g)": <p>,
       "Carbs (g)": <c>,
       "Fat (g)": <f>,
       "Calculated": "__YES__"
     }
   ```

4. If there are no un-calculated entries, do nothing.

## Output

One short line: how many meals were calculated and their names, or "No new meals to calculate." If a description was too vague, still give a best-effort estimate and note the assumption.

## Notes

- These are estimates; portions without grams are assumed at typical serving sizes.
- This is the on-demand version of the nightly scheduled task `meals-auto-calc` (runs 21:00 daily).
