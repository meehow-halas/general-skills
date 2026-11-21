# `_learnit`: completion criteria

Date: 2026-11-21. Skill: `skills/learnit/`. The skill is complete when all criteria are PASS.

## Stop rule

- Verification runs in one pass. Fix only what fails a criterion.
- After a fix, repeat only the criteria that failed. At most 2 such passes. If they still fail, change the criterion or accept the state. Don't add new rules.
- New edge cases go to `docs/backlog/` (`_parkit`), not to the skill.
- A subagent gets the user's task and the skill, nothing more. The "learner's" answers are simulated by a separate prompt with a given level of knowledge.

## A. Structure

- [x] A1. `SKILL.md` is the only instruction file and has ≤ 190 lines.
- [x] A2. The symlink `~/.claude/skills/_learnit` points to `skills/learnit`, the skill visible in the session.
- [x] A3. Topic data goes to `~/.claude/learning/`, regardless of the working directory.

## B. Behaviour (scenarios)

- [x] B1. `start-it`: an IT topic (e.g. "async in Python"). One question per message with a recommendation, a diagnostic test before the plan, after approval `topic.md`, `plan.md`, `knowledge.md`, `journal.md` and an entry in `INDEX.md` are created.
- [x] B2. `start-humanities`: a non-technical topic (e.g. "causes of World War I"). Plan and verification without programming tasks; question types fit the domain (cause–effect, comparison, chronology).
- [x] B3. `check-mixed`: verification with partly wrong answers. Each concept gets its own status with evidence and a review date; "I understand" without an answer doesn't count.
- [x] B4. `support`: a concept failed twice. `support/NN-<stage>.md` is created with a diagnosis of the cause, a different approach, and re-verification.
- [x] B5. `resume`: a new session "back to <topic>": state restored from files alone; overdue concept reviews first, then the current stage.
- [x] B6. `expand`: the user raises a related thread. Proposal: a stage or a separate topic; the change recorded in scope history; existing stage numbers unchanged.
- [x] B8. `start-with-questions`: a first message with substantive questions and reference repositories. The first reply is a scope draft, questions assigned to areas, no substantive answers (Haiku and Sonnet).
- [x] B9. `lesson-flow`: the plan goes beyond the learner's questions; before the first check question a lesson in `lessons/` with verified sources is created; the question has a scenario and an explicit expectation; a correct short answer → follow-up, not a lowered grade.
- [x] B10. `mentor-style`: with the global rule "extremely concise" the conversation is still in full sentences, no statuses in chat; error → hint before the solution; feedback: what's good → what's missing → next step.
- [x] B11. `export`: a file in `exports/`, lessons + key + tutor prompt; no progress, profile, journal, paths, or personal data (grep 0 hits).
- [x] B12. `recipient`: an assistant without _learnit with the export file and a progress card writes the next stage's lesson from the sketch, fitted to the card; tone without labels; card at the end of the session.
- [x] B7. `status`: the question "what do I know about <topic>?": read-only, answer from `knowledge.md`.

## C. Critical rules

- [x] C1. No session time limit: the skill imposes no time or number of stages per session.
- [x] C2. State saved after each verification: an interrupted session loses nothing.
- [x] C3. No git: the skill runs no `git init` or commits in `~/.claude/learning/`.
- [x] C5. Checks and reviews are a proposal: the user may skip them, and a stage spans many sessions without losing state.
- [x] C4. Practical exercises (files) only in `<slug>/exercises/`.

## D. Real use

- [ ] D1. One real topic worked through by the user over ≥ 3 sessions, with no skill fixes along the way. Notes to the backlog.

## Verification result: 2026-11-21

A1–A3, B1–B7, C1–C5: PASS in one pass, with no skill fixes. Tests on copies of data in the scratchpad (overridden data directory); the real `~/.claude/learning` untouched.

Evidence:
- A1: 103 lines. A3: all runs wrote to the data directory, not the working directory.
- B3: "I understand, you don't need to ask" → asked anyway, status `unknown`.
- B6: headings of stages 01–04 unchanged, new 05.
- B7 / C2: file checksums before and after identical; B5: state saved before "I have to run".
- C1: grep of transcripts (minutes/hours/schedule/deadline): 0 hits. C3: no `.git`. C4: non-md files only in `exercises/`.

Ambiguities reported by testers → `docs/backlog/learnit-test-round-1-gaps.md`. D1 remains.

## Fix v0.1.1 and repeat of B3–B5: 2026-11-21

Implemented items 1–5 from the backlog (intervals with a `step` column, statuses, sources, support trigger, diagnosis). SKILL.md: 109 lines (A1 OK). B3–B5 repeated on fresh data copies: PASS.

Interval consistency: expected values written out before the test, all matched:
- B3: task step 2 → 11-24; create-task step 1 → 11-22; gather, concurrency step 1 → 11-22. Support proposed, not started.
- B4: task step 2 → 11-24. Support proposed first; file `support/02-*`; source verified on the web.
- B5: await, task step 2 → 11-24; event-loop step 3 → 11-28; create-task step 1 → 11-22. Migration of the `step` column consistent across 3 testers.

New notes → backlog items 12–16. D1 remains.

## Fix v0.1.2: 2026-11-21

Real use (Haiku 5.5): the skill answered the start questions on substance. Added the "don't teach at the start" rule and a scope draft from the first message. B8 on Haiku and Sonnet with the original prompt: PASS: 0 substantive answers, questions recorded verbatim in `topic.md` and assigned to areas, one question about a gap. SKILL.md: 112 lines.

## Fix v0.1.3: 2026-11-21

Real use (Haiku, prompt without `/_learnit`): the skill wasn't invoked. Changed `description` ("invoke first…"). `claude -p --model haiku` measurement: full prompt 0/3 → 4/4, short 2/2, resume 2/2, negative 0/2. Confirmed by the user in a new Haiku session. D1 remains.

## Fix v0.2.0: 2026-11-21

Real use: the program narrowed to learner questions, no lesson (questions right away), questions without context, a grade lowered for an unrequested justification, content unsupported by sources. B9 on Haiku: PASS: 6 stages (3 beyond the questions), lesson 01 (706 words, source: official documentation, verified), a question with a scenario and "2–3 sentences", follow-up "why?" before an `ok` grade. SKILL.md: 128 lines. D1 remains.

## Fix v0.3.0: 2026-11-21

User note: the style was stiff and discouraging. Added the "Mentor style" section (sources: `docs/learnit-references.md`). B10 on Haiku with the "extremely concise" rule: PASS. Full sentences, checking introduced as practice, on error a hint pointing to an example from the lesson, statuses not announced, a progress summary at the end. Fix after the test: a concept identifier leaked into chat; a ban on identifiers added. A1 raised to ≤ 160 lines.

## v0.3.x–0.4.0: 2026-11-21

0.3.2: the "shall we start?" question after the plan. 0.3.3: triggering by intent (Haiku: "I'd like…" 3/3, with a typo 3/3, EN 2/2, negatives 0/4). 0.4.0: export; B11 on Haiku PASS. A1 raised to ≤ 180 lines.

## v0.4.1–0.4.2: 2026-11-21

Export without writing lessons (lessons are written on the fly for the recipient), sketches, a "Method" section, a progress card, a tutor prompt template. B11 (again) and B12 on Haiku: PASS. First attempt at B12 (prompt composed by the model): mechanics OK, tone stiff, so the template was introduced.

## v0.5.0: 2026-11-21

Language-agnostic rewrite: skill content in English, structure fixed in English, content in the user's language. Behaviour scenarios not re-run: **open item**, re-run B1, B3, B5, B11 with a non-English learner before treating v0.5.0 as verified.

## v0.5.0–0.5.1 — 2026-11-21

After the English translation (0.5.0), regression on Haiku: Polish triggering (learning phrases 11/11, negatives 0/4), Polish start flow, Polish export from English templates (recipient instructions 19/19 items, tutor prompt 20/20): PASS. Found: the structure rule was ambiguous (mixed-language headings; migration of an older topic silently dropped a section). 0.5.1: canonical structure per state file, reader-facing headings in the topic language, `new` concept status, migration that never drops content. Re-test on Haiku: new topic with canonical structure and Polish lesson headings; migration of a copy of real Polish-structured topics with unmapped sections kept at the end and a journal note: PASS. SKILL.md: 181 lines, A1 raised to ≤ 190.
