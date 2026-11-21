# _mapit

Plans any undertaking (code, migration, move, training, event) in stages, in files, with pause and resume.

## Usage

"plan…", "break it into stages…", "what's next in the plan?". Can start from an idea parked in `docs/backlog/` (`_parkit`). "On your own" / "no questions" switches to autonomous mode.

## Phases

1. **Plan**: one question at a time with a recommendation (`Q<n>`), split into stages, approval.
2. **Execution**: gate (plan complete, previous stage `done`), run by `agent` / `user` / `mixed`, verification `PASS`/`GAP` with evidence.
3. **Query**: read-only; status, gaps, whether the next stage can start.

## Files

`docs/plans/<slug>/`:
- `README.md`: goal, stage table, decisions, assumptions
- `NN-<stage>.md`: spec with acceptance criteria
- `NN-<stage>.brief.md`: prompt for the executing agent

Finished plans go to `docs/plans/archive/<slug>/`. Stage statuses: `planned`, `in progress`, `gaps`, `done`.

## More

- Skill definition: [skills/mapit/SKILL.md](../skills/mapit/SKILL.md)
- Acceptance criteria: [docs/mapit-acceptance-criteria.md](../docs/mapit-acceptance-criteria.md)
- Changes: [CHANGELOG.md](../CHANGELOG.md)
