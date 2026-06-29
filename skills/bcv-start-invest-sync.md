# BCV Start Invest Sync Skill

**Purpose**  
Automated daily (or on-demand) sync that detects "BCV Start invest" expenses in the Finance Tracker Transactions database and accumulates the invested amount on the BCV Start Invest asset page.

**Math**  
Base: 21,000  
Every matching expense of 300 → new total = previous total + 300  
Example: 21,000 → 21,300 → 21,600 etc.

## Operating Rules (from AGENTS.md)
- Never assume state or intent — always verify.
- In interactive mode: propose changes only, never apply without explicit "go".
- For automated/scheduled runs: log every action with timestamp, amount, and new total.
- Be idempotent: never double-process the same transaction.

## Data Sources
- **Transactions Database** (Expenses view):  
  https://www.notion.so/41209dd88306838699740163f25651de?v=e6209dd883068345873008058a303daa
- **BCV Start Invest Asset Page**:  
  https://www.notion.so/BCV-Start-Invest-37709dd883068089903bd87e116aa04a

## Logic Flow
1. Read the current "Last Sync" timestamp (stored on the asset page or in a dedicated log).
2. Query Transactions for:
   - Name contains "BCV Start invest" (case-insensitive)
   - Type = 🚥 Expense
   - Date & time > Last Sync
3. For each matching transaction:
   - Add the `Amount` to the tracked total on the BCV Start Invest page.
   - Update the Last Sync timestamp to the transaction date (or current time).
4. Log the run (date, amounts processed, new total, any errors).

## Properties to Update (to be confirmed/adjusted)
- Target property on BCV Start Invest page that holds the accumulating total (currently showing ~21,000 base, needs to become 21,300 etc.).
- Recommended: Add or use a number property called **"Total Invested"** or **"Accumulated Value"** if not already present.
- "Last BCV Sync" date property on the same page (for state).

## How to Use
### Manual / Interactive
Call this skill and provide confirmation before any write.

### Automated (Recommended)
- Schedule daily (nightly or on system wake-up) via Grok recurring task or a calling agent.
- The skill runs in "auto" mode with full logging.

## Logging Recommendation
Create or use a simple "BCV Sync Log" page/database to record every run for auditability.

## Future Extensions
- Support multiple investment amounts per month.
- Add notifications on successful sync.
- Handle currency conversion if needed.
- Integrate with other asset trackers.

---
**Status**: Draft — ready for refinement after first test run.
**Created**: 2026-06-30
**Owner**: Loris Impinna