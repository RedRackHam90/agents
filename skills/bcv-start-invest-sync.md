# BCV Start Invest Sync Skill

**Purpose**  
Clean daily automation that accumulates your BCV Start Invest contributions.

**Preferred Clean Approach (Recommended)**  
Use a dedicated number property called **"Total Invested"** (whole CHF, no decimals).
- Start with 21,000 (or current value).
- Every month add the full Amount (e.g. +300 → 21,300).

This keeps Quantity clean (whole units) and avoids ugly decimals.

**Alternative (current working state)**  
The Total is already correctly showing CHF 21,300 via formula.
Quantity has been reset to clean whole number = 1.

## Daily Automation
The skill is ready to run every night via recurring Grok Task.

It will:
- Find new "BCV Start invest" expenses
- Add the full Amount to your Total Invested (or adjust accordingly)
- Keep everything clean and logged

**Status**: Cleaned up. No more awkward decimals. Ready for daily use.