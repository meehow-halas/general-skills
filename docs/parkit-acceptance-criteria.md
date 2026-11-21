# `_parkit`: completion criteria

Date: 2026-11-17. Skill: `skills/parkit/`. The skill is complete when all criteria are PASS.

Goal: a simple, predictable scratchpad of ideas. Priority: reliability and simplicity, not edge-case coverage.

## Stop rule

- Verification in one pass. Fix only what fails a criterion.
- After a fix, repeat only the criteria that failed. At most 2 such passes. If they still fail, change the criterion or accept the state. Don't add new rules.
- A fix may not lengthen `SKILL.md` beyond the A1 limit. Better to remove a rule than add one.
- New edge cases go to `docs/backlog/`, not to the skill.
- Tests in normal mode, without hunting for ambiguities. A subagent gets the user's task and the skill, nothing more.

## A. Structure (checked by commands)

- [x] A1. `SKILL.md` is the only instruction file of the skill and has ≤ 120 lines.
- [x] A2. No contradiction with `_mapit`: the file format contains the sections `_mapit` reads (Problem / goal, Proposed solution, Acceptance criteria, Open questions, Related files, History); no prohibition clashing with the `Source` field.
- [x] A3. The skill `_parkit` is visible in the session (`~/.claude/skills/_parkit/SKILL.md` points to the file in the repo).

## B. Behaviour (scenarios from `skills/parkit/evals/evals.json`, run once)

- [x] B1. `park-from-conversation`: all expectations met.
- [x] B2. `nothing-to-park`: all expectations met.
- [x] B3. `dedup`: all expectations met.
- [x] B4. `sanitization`: all expectations met.
- [x] B5. `review-and-return`: all expectations met.
- [x] B6. `review-empty`: all expectations met.

## C. Reliability (hard limits, checked after B)

- [x] C1. In no scenario was a file created or changed without prior approval of the preview.
- [x] C2. In no scenario were files outside `docs/backlog/` changed or a git operation run.

## D. Real use (after A–C)

- [ ] D1. One real idea parked by the user and later used as `_mapit` input, with no skill fixes along the way. Notes go to the backlog.

## Verification result: 2026-11-17

A1–A3, B1–B6, and C1–C2: PASS, in one pass, with no skill fixes. 6 fresh `general-purpose` agents, each in a separate test repo, user answers simulated.

Evidence from files on disk (checksums before/after):
- B1: only `docs/backlog/cache-for-report-queries.md` was created at the repo root (cwd was `src/`); a location question before `docs/`.
- B2, B6: no `docs/`, no changes.
- B3: only the existing file changed; a new entry in "History"; no new file.
- B4: grep for surname, company, e-mail, phone, token, and host over `docs/` gave 0 hits.
- B5: checksums of both files unchanged; a table with `→ plan report-cache`.
- C1: a preview before every save. C2: changes only in `docs/backlog/`, 0 commits in all repos.

D1 remains.

## Language-agnostic rewrite: 2026-11-21 (v0.2.0)

Skill content translated to English; structure fixed in English, content follows the conversation language. B/C not re-run.
