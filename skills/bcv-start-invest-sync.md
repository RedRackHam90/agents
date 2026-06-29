# BCV Start Invest Sync Skill

**Goal**  
Whenever there is a **new** "BCV Start invest" expense entry (by date), add its full Amount to the tracked total value. Only new entries — never re-process old ones.

**Current State**  
- Total value is now correctly at **CHF 21,300** (today's 300 CHF expense included).
- Quantity adjusted to ~1.0142857 so the formula Total reflects the accumulated value.

## Rules for the Task / Skill
- Only process expenses where `Date & time` > Last Sync date.
- Add the full Amount to the tracked total.
- Update Last Sync to the latest processed date.
- Log what was done.

## How the Daily Task Should Work
1. Check for new "BCV Start invest" expenses since last run.
2. For each new one: add Amount to total value.
3. Never touch old entries.

**Status**: Fixed. Today's entry is included. Future runs will only catch new dated entries.