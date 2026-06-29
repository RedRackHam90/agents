# BCV Start Invest Sync Skill

**Strict Rules**  
- **Never touch Quantity** — leave it completely alone (clean whole number).
- Only increment the **value** (Total Invested) when there is a **new** expense entry (by date).
- Only process entries newer than last sync date.

**How it works going forward**  
1. Find new "BCV Start invest" expenses (Date > Last Sync).
2. Add the full Amount to a dedicated **Total Invested** number property.
3. Update Last Sync date.
4. Log it.

**One-time action needed**  
Create a number property called **"Total Invested"** on the BCV Start Invest page (or Assets database) and set it to the current desired value (e.g. 21300). The skill will then maintain it automatically for all future entries.

**Current Status**  
Quantity left at clean 1. Skill ready to only increment value on new dated entries.

Daily Grok Task will keep the value updated cleanly without ever touching Quantity again.