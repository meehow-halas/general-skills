# `_mapit`: completion criteria

Date: 2026-11-17. Skill: `skills/mapit/`. The skill is complete when all criteria are PASS.

## Stop rule

- Verification runs in one pass. Fix only what fails a criterion.
- After a fix, repeat only the criteria that failed. At most 2 such passes. If they still fail, change the criterion or accept the state. Don't add new rules.
- New edge cases found along the way go to `docs/backlog/` (`_parkit`), not to the skill.
- Tests in normal mode, without hunting for ambiguities and without executing "literally". A subagent gets the user's task and the skill, nothing more.

## A. Structure (checked by commands)

- [x] A1. `SKILL.md` is the only instruction file of the skill and has ≤ 120 lines.
- [x] A2. No references to removed files and concepts (`references/`, `waiting`, `skipped`, `critical`).
- [x] A3. The symlink `~/.claude/skills/_mapit` points to `skills/mapit`, and the skill is visible in the session.

## B. Behaviour (scenarios from `evals/evals.json`, run once)

- [x] B1. `new-code-plan`: all expectations met.
- [x] B2. `non-code-plan`: all expectations met.
- [x] B3. `seed-from-backlog`: all expectations met.
- [x] B4. `resume-draft`: all expectations met.
- [x] B5. `autonomous`: all expectations met.
- [x] B6. `query-status`: all expectations met.

## C. Regressions from rounds 1–4 (the valuable core)

- [x] C1. Consent before an action: in `autonomous`, when a project rule requires consent for a version bump, `VERSION` doesn't change before consent and the stage doesn't get `done`.
- [x] C2. Fixed numbers: adding a stage to a closed plan gives the next free number and doesn't rename existing files.
- [x] C3. Resume: a plan interrupted in `draft` is continued in a new session from the files alone, without repeating settled questions.
- [x] C4. Sanitisation: a plan from a backlog containing a surname, phone, e-mail, and account number. Grepping the plan files for that data gives 0 hits.
- [x] C5. An `agent` stage in a repo: tests are actually run and quoted, and verification is done by a fresh `Agent`.

## D. Real use (after A–C)

- [ ] D1. One real plan carried out by the user to the end, with no skill fixes along the way. Notes go to the backlog.

## Verification result: 2026-11-17

A1–A3, B1–B6, and C1–C5: PASS, in one pass, with no skill fixes.

Evidence from files on disk:
- C1: `VERSION` = 0.1.0, stage `in progress` with a note "awaiting consent".
- C4: grep for personal data in the plan files gave 0 hits.
- C5: `Ran 4 tests … OK`, verification by a fresh `Agent`.
- C2: new stage `03-*`, existing file names unchanged.

D1 remains.

## Fix after verification: 2026-11-17

Implemented the backlog item `mapit-readme-template-gaps` (v0.1.1): an "Assumptions" section in the README template; "End of planning" removes the "Open questions" section. SKILL.md: 110 lines (A1 still OK). B/C criteria were not repeated: the change doesn't touch their behaviour. D1 remains.

## Language-agnostic rewrite: 2026-11-21 (v0.2.0)

Skill content translated to English; structure fixed in English, content follows the conversation language. B/C not re-run. The line limit in A1 is unchanged (SKILL.md ≈ 110 lines).

## v0.2.1 — 2026-11-22

`description` shortened to 401 characters, trigger front-loaded. Triggering on Haiku, old vs new: "plan this… stages" and "what's next in the plan" invoked on both; a request to break an office move into stages mostly answered directly (new 1/5, old 0/2). B/C not re-run: the body is unchanged.
Sonnet, old vs new: all mapit prompts invoked (office move 2/2, team training plan 2/2), a language-learning plan went to learnit.
