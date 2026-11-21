---
title: "_learnit: ambiguities from test round 1"
type: fix
date: 2026-11-21
source: verification B1–B7 of the _learnit skill (all PASS, testers' notes)
tags: [learnit]
---

> Note: written before the v0.5.0 rename; today `krok` is `step`, "Po" is `After`, "niezweryfikowane" is `unverified`.

## Context
All criteria A–C passed. Testers reported ambiguities; they resolved them sensibly but differently.

## Problem / goal
Unify behaviour where testers guessed. Priority by number of reports.

## Proposed solution
1. **Review intervals** (B3, B4, B5): an explicit step rule: first `ok` → +1 day; each next `ok` → next step 3/7/21; error → reset to 1 day, status `shaky`.
2. **Sources** (B2): verify titles, links, editions on the web or mark "unverified".
3. **Support trigger** (B3, B4): offer support (don't start without asking); threshold: 2nd failed attempt at a concept or a stage in `review`. File name: the number of the stage with the difficulty.
4. **`unknown` vs `shaky`** (B3): `unknown` = no correct elements; `shaky` = partly correct.
5. **Diagnosis result** (B1, B2): record in `knowledge.md` marked "diagnostic", no review date. Diagnostic questions open, without options.
6. **"After" field** (B2, B6): add to the stage template; for equal "After", order by number.
7. **Scope** (B1): accept the scope with one question before the plan.
8. **`profile.md`** (B1, B2): create at the first topic with preferences from the start conversation.
9. **Directories** (B2): create `support/` and `exercises/` only on first use.
10. **Reviews in check** (B3, B4): offer also at the start of check; skipping doesn't change the date.
11. **Status** (B7): may end with one question about the next step; report inconsistent data, don't fix it.

From the B3–B5 repeat (2026-11-21):
12. **Promotion after support** (B4r): `ok` right after an error the same day gives step 2 (3 days); consider `ok` in the same session as an error giving only step 1.
13. **Choice of reviews** (B5r): with > 3 overdue, which to pick (suggestion: `shaky` + oldest); a concept from the current check doesn't count as a review.
14. **"You don't have to ask"** (B3r): ask anyway or treat as a skip.
15. **`review` stage in INDEX** (B3r): whether to show the stage status in the "stage" column.
16. **Data consistency** (B5r, B7): a stage `done` with a key concept that dropped to `shaky`: report it or change the status.

## Rejected alternatives
- Full SM-2 algorithm: too heavy to start.

## Acceptance criteria
- SKILL.md ≤ 140 lines after the changes.
- Repeated B3–B5 give the same intervals across testers.

## Related files
- `skills/learnit/SKILL.md`
- `docs/learnit-acceptance-criteria.md`

## History
- 2026-11-21: created
- 2026-11-21: items 1–5 implemented in v0.1.1; B3–B5 repeated: intervals as expected across 3 testers; added items 12–16
