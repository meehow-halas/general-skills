# _parkit

A scratchpad of ideas in the repo: findings from a conversation saved for later as `.md` files in `docs/backlog/`. No statuses, no tracker.

## Usage

On request only. "park this", "save for later", "show parked ideas", "go back to the idea about…", "delete…".

## Intents

- **Park**: preview, save after approval; deduplicated against existing files.
- **Review**: table (date, type, title, file).
- **Revisit**: load and summarise; checks that `path:line` references are still valid.
- **Edit / delete**: only after a preview and explicit confirmation.

## File

`docs/backlog/<short-name>.md` with frontmatter (`title`, `type`: `feature|fix|optimization|idea`, `date`, `source`, `tags`) and sections: Context, Problem / goal, Proposed solution, Acceptance criteria, Open questions, History.

Secrets, personal data, and internal URLs are sanitised. No git operations.

## Next

Turning an idea into stages: [_mapit](mapit.md).

## More

- Skill definition: [skills/parkit/SKILL.md](../skills/parkit/SKILL.md)
- Acceptance criteria: [docs/parkit-acceptance-criteria.md](../docs/parkit-acceptance-criteria.md)
- Changes: [CHANGELOG.md](../CHANGELOG.md)
