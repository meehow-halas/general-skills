# Changelog

Format: Keep a Changelog. Package releases come first; per-skill history (the versions the skills went through before and alongside the package) follows.

## 0.2.0 — 2026-11-21

### Added
- Repository docs: `README.md`, `guide/` (one page per skill), `AGENTS.md` (`CLAUDE.md` symlinks to it), this changelog.

### Changed
- All skill content, docs, and evals translated to English. Skills are language-agnostic: they talk in the user's language and understand intent in any language. Structure (headings, field names, statuses) is fixed English; free text follows the conversation language. See skill history below: learnit 0.5.0, mapit 0.2.0, parkit 0.2.0.
- Per-skill changelogs merged into this file.

## 0.1.0 — 2026-11-21

### Added
- Initial release: skills `learnit`, `mapit`, `parkit` and the installer `general-skills` (`install`, `update`, `uninstall`, `list`; harnesses Claude Code, Cursor, Codex, OpenCode).

## Skill history

Skill versions are independent of the package version. Entries before 0.5.0 / 0.2.0 were written in Polish and are translated here.

### learnit

#### 0.5.0 — 2026-11-21

- Skill content translated to English (`SKILL.md`, `README.md`, `export-readme.md`, `export-tutor-prompt.md`). The skill is language-agnostic: it talks in the user's language and understands intent in any language. Structure stays fixed English across languages (section headings, table columns, status values), free text follows the topic language. `description` rewritten in English and matches learning intent in any language.
- Renamed in files: `krok` → `step`, `Pytania ucznia` → `Learner questions`, `Historia zakresu` → `Scope history`, `Po` → `After`, `niezweryfikowane` → `unverified`, `Klucz odpowiedzi` → `Answer key`.

#### 0.4.3 — 2026-11-21

- Export starts with recipient instructions from the fixed template `export-readme.md` (what this is, how to use it with and without AI, progress card, good to know, contents). One file instead of a separate README so nothing gets lost when sending and pasting. Haiku test: template copied in full, placeholders filled, 0 private data.

#### 0.4.2 — 2026-11-21

- The tutor prompt is a fixed template `export-tutor-prompt.md`, copied in full (conversation, lesson, and checking rules, an "instead → better" example, the progress card format). Reason: a prompt composed anew dropped the style rules and the recipient's assistant returned to a stiff tone ("Card received", labels "Good: / Missing:"). Recipient test on Haiku (without _learnit, file + card): natural tone, choice with recommendation, lesson 02 written from the sketch with a hook and fitted to the difficulty from the card, questions after "I've read it", follow-up "why?" instead of pointing out a gap, card at the end.

#### 0.4.1 — 2026-11-21

- Export: missing lessons are not written before exporting (lessons are written on the fly and fitted to progress, also for the recipient); the question about writing them removed. New in the file: sketches of stages without a lesson, a "Method" section (rules from README and "Mentor style" + foundations with links), a progress card (the tutor prompt asks for it at the start and writes it out at the end of the session) as memory between conversations; the tutor writes a lesson from the sketch fitted to the card.

#### 0.4.0 — 2026-11-21

- `export` mode: one self-contained Markdown file `<slug>/exports/<slug>-YYYY-MM-DD.md` for someone without _learnit. Contains the plan, finished lessons, exercises, "Check yourself" with the key in `<details>`, and at the end a tutor prompt for any AI assistant (for stages without a lesson the assistant writes them from the plan). When lessons were missing the skill asked what to do. No progress, profile, journal, or support; examples from private materials rewritten to general ones. Described in README (section 9). Haiku test: export of 1569 words, grep for personal data and repository paths gave 0 hits.

#### 0.3.3 — 2026-11-21

- `description`: triggering on learning intent in any form, language, and with typos ("I'd like to learn…"), also when the topic looks like a short definition. Reason: sessions "Front-loading and RAG in AI 1/2" (Haiku): a typo'd "I'd like to learn…" did not invoke the skill. Haiku measurement: "I'd like…" 3/3, typo 3/3, English 2/2, full skills prompt 2/2; negatives "What is RAG?" and "Explain closure" 0/4 (correct). Description: 1255 characters (listing limit 1536).

#### 0.3.2 — 2026-11-21

- After plan approval the skill asks "start now / later" instead of writing lesson 01 right away (session "Using skills in AI 4").

#### 0.3.1 — 2026-11-21

- `README.md`: teaching rules in accessible language (start, program, lessons, checking, help, reviews, pace, scope changes, commands, data, scientific basis). `about` mode in SKILL.md: a question about the method → an answer from the README in the conversation language. Trigger in `description`. Answer in the learner's language (no statuses or state files); when README is unavailable, from SKILL.md. Haiku test (`claude -p`): skill invoked 3/3, answer from README accessible.

#### 0.3.0 — 2026-11-21

- "Mentor style" section based on research (details in `docs/learnit-references.md`): INSPIRE model (Lepper), personalization principle (Mayer), feed up/back/forward feedback (Hattie & Timperley), low-stakes retrieval, SDT (Ryan & Deci). Conversational tone instead of protocol, no process language or identifiers in chat, choice for the learner, a hook at lesson start, guiding questions and gradual hints, checking as practice, three-move feedback, reflection, visible progress at the end. In learning mode the style takes precedence over global brevity rules. Concept status saved in the file, not announced in chat.

#### 0.2.1 — 2026-11-21

- Languages (language-agnostic rule): file and folder names always English regardless of conversation language (kebab-case, with an example), content always in the conversation language the topic was started in (`Language:` in `topic.md`). Reason: the v0.2.0 test created `lessons/01-anatomia-skilla.md`.

#### 0.2.0 — 2026-11-21

- After real use (topic "skills in AI"): scope = a map of the whole domain, learner questions are emphases, not a boundary. Stage = lesson + exercises + check; the lesson in `lessons/NN-<stage>.md` (why, explanation with context, examples, common mistakes, answers to learner questions, summary, verified sources, exercises) and in full in chat; questions only after "I've read it". Source-based content, unverified marked. Check questions: a scenario with context + explicit expectation; grading by what was asked, follow-up before lowering. Haiku test: a 6-stage plan (beyond the learner questions), a 706-word lesson with a documentation source, follow-up before grading.

#### 0.1.3 — 2026-11-21

- `description`: an "invoke first" instruction at the start, with an explicit case of a message with questions and reference repositories. Haiku measurement (`claude -p`): the full prompt from the session 0/3 → 4/4; short 2/2 → 2/2; "back to learning" 2/2; negative "explain closure" 0/2 (correct).

#### 0.1.2 — 2026-11-21

- After the first real use: at the start the skill doesn't teach: substantive questions from the first message go to `topic.md` ("Learner questions") and to plan stages. The first reply is a scope draft from the message, then questions only about gaps. A diagnostic test skippable when the level follows from reference materials. Stronger `description`.

#### 0.1.1 — 2026-11-21

- After test round 1 (backlog `learnit-test-round-1-gaps`, items 1–5): a `step` column and an explicit interval rule (ok → step +1, error → step 1, skip unchanged, `mastered` after step 4); definitions of `unknown`/`shaky`/`ok`; sources verified or `(unverified)`; support proposed first, trigger and file name; diagnosis results in `knowledge.md` (step 0, no date); answers in learn are evidence; reviews offered in check too.

#### 0.1.0 — 2026-11-21

- First version: modes start / plan / learn / check / support / expand / status / resume; global data stored locally in `~/.claude/learning/` (no git); material per stage, not per session; checks and reviews on request; concept map with 1/3/7/21-day reviews; soft 80% gate; learner profile shared across topics; no time limits; domain-agnostic.

### mapit

#### 0.2.0 — 2026-11-21

- Skill content translated to English. The skill is language-agnostic: it talks in the user's language and understands intent in any language. Structure fixed in English (README template headings `Goal`, `Source`, `Open questions`, `Stages`, `Decisions`, `Assumptions`; statuses), content follows the conversation language. `Źródło` → `Source`, `autonomicznie` → `(autonomous)`.

#### 0.1.1 — 2026-11-17

- README template: an "Assumptions" section. "End of planning": remove the "Open questions" section instead of clearing it.

#### 0.1.0 — 2026-11-17

- First version. Based on `_make-plan` (se-harness): stages in files, `draft`/`complete` state in the README, one question with a recommendation, a gate between stages, verification by a fresh agent, query mode, archiving.
- Compared to `_make-plan`: any domain (stage executor `agent`/`user`/`mixed`, criteria as checkboxes, "Detailed plan"), `autonomous` mode and decision numbers `Q<n>` (from `planit`), start from a `_parkit` idea, location from project rules, fixed stage numbers, consent before an action, sanitisation.
- Simplified after 4 test rounds: one file instead of `SKILL.md` + `references/`; dropped among others the `critical` mode, statuses `waiting`/`skipped`/`abandoned`, elaborate decision markers and edge-case rules (a copy of the expanded version kept outside the repo).

### parkit

#### 0.2.0 — 2026-11-21

- Skill content translated to English. The skill is language-agnostic: it talks in the user's language and understands intent in any language. Structure fixed in English (frontmatter keys, section headings `Context`, `Problem / goal`, `Proposed solution`, `Rejected alternatives`, `Acceptance criteria`, `Open questions`, `Risks`, `Related files`, `History`), content follows the conversation language.

#### 0.1.1 — 2026-11-17

- Consistency with `_mapit`: review marks items moved to a plan (`→ plan <slug>`), return points to `_mapit` for breaking into stages.
- Removed the rule "don't add links to the backlog in other documents": the ban on changes outside `docs/backlog/` covers it; it clashed with the `Source` field in `_mapit`.
- Added `evals/evals.json` and `docs/parkit-acceptance-criteria.md`.

#### 0.1.0 — 2026-11-16

- First version: park, review, return, change/delete; preview before saving, deduplication, sanitisation, one `.md` file per topic in `docs/backlog/`.
