---
name: weekly-meal-plan
description: Create next week's 7-day meal plan in Notion Health Tracker OS (~3,027 kcal/day, maintain)
---

Create next week's meal plan (Monday through Sunday, the 7 days starting tomorrow) in Loris's Notion "Health Tracker OS".

CONTEXT
- Day meals data source: collection://99f09dd8-8306-8396-a42f-07bac4db268f. Schema: Name (title), Date (date), Breakfast / Lunch / Dinner (relations to Recipes data source collection://ae509dd8-8306-82b4-b596-87809ec7f558), Additional (relation to Ingredients data source collection://4bd09dd8-8306-82a0-b0f5-8711258ccc8f).
- Entries with a Date automatically appear in the Calendar's "Day meal plans" view; no extra step needed.
- Daily target (Maintain, trains daily): ~3,027 kcal, ~227g protein, ~303g carbs, ~101g fat.

STEPS
1. Check the Day meals data source (notion-search with data_source_url) for existing entries on the target dates — skip any date already planned, never duplicate.
2. Fetch the Recipes data source to get current recipes with their Calories and meal tags (🍳 Breakfast / 🥗 Lunch / 🌙 Dinner). Use any newly added recipes too.
3. Create one page per day, named after the weekday (Monday, Tuesday, ...), icon 🍽️, with Date set:
   - Breakfast relation: one breakfast recipe + the "Post-Workout Power Shake" recipe (he trains daily).
   - Lunch: one lunch-tagged recipe. Dinner: one dinner-tagged recipe.
   - Rotate recipes for variety: never the same lunch or dinner two days in a row, spread all recipes across the week.
   - Additional relation: snack ingredients (mixed nuts, skyr, Greek yogurt, protein bars, banana, honey, peanut butter, mixed berries) chosen so the day total reaches ~3,000–3,050 kcal.
   - Page content: a bold target line, a bullet list of the meals with their kcal, a snack line with exact portions and kcal estimates, and a bold day total line confirming ~3,027 kcal is met.
4. Double-check each day's arithmetic before creating the page.

OUTPUT
Reply with a short summary: dates planned, total kcal per day, and any recipes newly used.
