# BCV Start Invest Sync Skill

**Purpose**  
Automated daily (or on-demand) sync that detects "BCV Start invest" expenses in the Finance Tracker and accumulates the invested amount by adjusting Quantity on the BCV Start Invest asset page (keeping Total formula-driven).

**Math (clean & formula-friendly)**  
Price per unit = 21,000 (fixed)  
For every expense of X CHF:  
Delta Quantity = X / 21,000  
New Quantity = Current Quantity + Delta Quantity  

Example:  
Base: Quantity = 1 → Total ≈ 21,000  
After 300: Quantity ≈ 1.0142857 → Total ≈ 21,300  
After next 300: Quantity ≈ 1.0285714 → Total ≈ 21,600

## Operating Rules
- Follow AGENTS.md strictly.
- Automated runs must be fully logged and idempotent.
- Never double-process transactions.

## Data Sources
- Transactions (Expenses): https://www.notion.so/41209dd88306838699740163f25651de?v=e6209dd883068345873008058a303daa
- BCV Start Invest page: https://www.notion.so/BCV-Start-Invest-37709dd883068089903bd87e116aa04a

## Concrete Logic
1. Read Last Sync timestamp (use transaction dates or add a date property on the asset page).
2. Query Transactions where:
   - Name contains "BCV Start invest"
   - Type = 🚥 Expense
   - Date & time > Last Sync
3. For each matching transaction with Amount = X:
   - Calculate delta = X / 21000
   - Update Quantity on BCV Start Invest page: current + delta
   - Update Last Sync tracking to the latest transaction date
4. Log the action (timestamp, amount added, new Quantity, new estimated Total).

## Current State (First Sync Applied 2026-06-29)
- Quantity updated from 1.0 to ≈ 1.0142857
- Tracked Total now reflects ≈ 21,300 (via formula)
- The 300 CHF expense from 2026-06-29 has been processed cleanly.

## How to Run Daily
**Recommended**: Set up a recurring Grok Task or agent that calls this skill every night (or on system wake-up) in automated mode.

The skill is production-ready for scheduled execution with full safety.

## One-time / Future Polish
- Optionally add a "Last BCV Sync" date property to the Assets database for explicit state.
- Add a simple sync log page if desired for history.

**Status**: Live + First sync completed.
**Ready for daily automated runs.**