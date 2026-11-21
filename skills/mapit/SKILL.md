---
name: mapit
description: Breaks any undertaking (code, migration, move, training, event) into stages in files under docs/plans/<slug>/, asking one question at a time with a recommendation; then executes the stages with a gate and verification and answers questions about plan status. Can start from an idea parked by _parkit (docs/backlog/). Use for map it out, plan this, break it into stages, what's next in the plan, in any language. Do NOT use for Jira/ADO tickets or a plain TODO list in the conversation.
---

# _mapit

A plan in stages, in files, with the ability to pause and resume. Three phases: **plan**, **execution**, **query**. Recognise them from intent. The skill is language-agnostic: talk to the user in their language, concisely, and understand their intent in any language. File content is in the conversation language unless project rules say otherwise. File names: English, kebab-case. Structure (headings, field names, statuses, `Planning: draft|complete`) is fixed English, used verbatim in every language.

**Mode:** `interactive` by default. When the user asks for independent work (e.g. "on your own", "no questions", in any language), use `autonomous`: don't ask, pick the recommendation and record the decision marked `(autonomous)`. Exceptions: things that need the user's consent (see Rules) and facts only they know.

## Location

- Project rules (`CLAUDE.md`/`AGENTS.md`) name a plans directory → use it.
- Otherwise in a repo: `<repo root>/docs/plans/<slug>/`, archive `docs/plans/archive/<slug>/`. Repo = the one the plan concerns (named, or the repo of the backlog file), not always the working directory.
- Outside a repo → ask; recommend `./plans/<slug>/`.

## Phase 1: Plan

### Start

- Plan directory exists → read `README.md` and continue. `Planning: draft` → ask the first open question; don't re-ask what's settled. Show a change to saved content as a diff before writing.
- Start from an idea in `docs/backlog/` (a `_parkit` file) → use it as input: goal, proposed solution, criteria, open questions (into the question queue), related files (check they are current). In the README write `Source: <path>`.
- In a code repo read the project rules and the relevant code (Grep/Glob first). Project rules beat guesses.
- Create `README.md` with `Planning: draft` after the first answer and update it after each one: an interrupted session loses nothing.

### Questions

- **One question per message**, `AskUserQuestion`, 2–4 options, the recommended one **first** with `(Recommended)` and the reason in its description.
- Every decision gets a fixed number `Q<n>` and goes into "Decisions" in the README.
- Ask only what changes the plan. Skip what context settles. Don't invent facts about the user (budget, deadlines, constraints): ask or record as an assumption.
- Questions end when the goal, scope, criteria, and split into stages are clear. Summarise the decisions in one short list.

### Stages

- One stage by default. Split only on a real dependency or a verifiable intermediate state (in plans spread over time: natural phases). Confirm the split with one question.
- Number `01`, `02`… in execution order. **Never renumber**; a stage added later gets the next free number.
- Every stage has an executor: `agent` (Claude), `user` (a human), or `mixed`.

### Files

`README.md`: index and state:

```markdown
# <Title>
Goal: <1–3 sentences>
Planning: draft | complete
Source: <sentence from the conversation | docs/backlog/<file>.md>

## Open questions
## Stages
| NN | Stage | Executor | Status | Verification |
## Decisions
- Q1: <decision> (<reason>)
## Assumptions
- <assumption> (omit the section when none)
```

Stage status: `planned` / `in progress` / `gaps` / `done`.

`NN-<stage>.md`: spec:
- Goal (1–3 sentences); Scope in / out (explicit); Decisions (`Q<n>`)
- Detailed plan: the substantive content the user asked for (breakdown, schedule, list), if the stage needs it
- Acceptance criteria: observable, as checkboxes `- [ ]` (in code: tests, contracts, files; outside code: a checkable fact)
- Verification: in code the tests to run (narrowest first); outside code: how the user will confirm
- Files / materials (paths); a version/CHANGELOG note if project rules require it
- Depends on: previous stage (`done`)

`NN-<stage>.brief.md`: only for `agent`/`mixed`: a self-contained prompt for the executor: goal, needed context, paths, the full spec text (copied), what not to change, constraints (no commits, no `.env`, no new dependencies or external actions without consent), definition of done.

Write only these files.

### End of planning

Show the file list and the stage table. Ask for approval (`autonomous`: skip). Then set `Planning: complete`, remove the "Open questions" section, and offer to start `01`. Don't start without consent unless the user asked for execution.

## Phase 2: Executing a stage

0. Gate: `Planning: complete` and the previous stage `done`. Otherwise `BLOCKED: <reason>. <what to do>`.
1. Status `in progress`.
2. Realisation:
   - `agent`: execute from the brief and spec, per project rules.
   - `user`: show the detailed plan and criteria as a checklist; wait for reports (also in later sessions). Tick each confirmed criterion in the spec right away.
   - `mixed`: both parts, in the order the dependencies dictate.
   - Questions along the way: as in phase 1; record the decision in the spec and README.
3. Verification:
   - `agent` part: automatically after realisation: one `Agent` (`general-purpose`, fresh context) gets the spec and brief paths and checks every criterion: `PASS` / `GAP` with evidence (`path:line`, command output); it edits no files. Run the spec's tests yourself and quote the real result.
   - `user` part: a criterion is `PASS` only after the user's explicit confirmation.
4. Result:
   - all `PASS` → `done`;
   - `GAP` or a red test → `gaps` and a list of gaps. One question: fix now (Recommended) or add a new stage. Don't widen scope silently.
   - A criterion awaiting the user's consent is not a gap: the stage stays `in progress` until consent is given.

## Query (any time)

Read-only: which stage is running, what's next, whether it can start, gaps, open questions.
- One plan → use it. Several → a question about all of them = an overview table; about one = ask which (recommendation: the one with a stage `in progress`). Skip `archive/`.
- Answer from `README.md`; read a spec only for the stage asked about. Quote statuses verbatim.
- "Can the next one start?" = yes only when `Planning: complete`, the previous is `done`, and the next is not `in progress`.
- Report a contradiction in the files, don't fix it. No edits, tests, or agents.

## Rules

- One question per message. Recommendation first and marked.
- Don't invent requirements. Mark an assumption as an assumption.
- **Consent before an action:** when project rules require consent (e.g. a version bump), and before a purchase, sending a message, or a booking, ask (`autonomous`: prepare it, add the criterion "user consent", and act only after consent).
- Don't write secrets or personal data (names, phones, e-mails, account numbers): replace with a description or placeholder.
- Files only in the plan directory. Exception with consent: one line in "History" of the source backlog file (`YYYY-MM-DD: moved to plan <slug>`).
- When all stages are `done`, offer (one question) archiving: move to `archive/<slug>/`, delete `*.brief.md`, fix links; for a plan with a `Source` in the backlog, also delete the backlog file.
- No commits, pushes, or PRs unless the user asks. Don't touch `.env`.
