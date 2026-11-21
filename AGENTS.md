# AGENTS.md

## Product

`general-skills` is a collection of general-purpose skills for AI agents (Claude Code, Cursor, Codex, OpenCode) plus a zero-dependency installer. Skills: `learnit`, `mapit`, `parkit`. The npm package is `general-skills`. The binary is `general-skills` (`bin/install.mjs`).

Behaviour of each skill is defined by `skills/<name>/SKILL.md`. Acceptance criteria live in `docs/<name>-acceptance-criteria.md`; they win over chat history. `docs/backlog/` holds parked ideas (`/_parkit`), not tickets: do not implement them "while here". `docs/learnit-references.md` is the research basis for `learnit`, not a source of norms.

## Layout

- `skills/<name>/` is the shipped skill: `SKILL.md` (required), optional `README.md`, support files, `evals/evals.json`.
- `bin/install.mjs` copies or symlinks `skills/<name>/` into global skill dirs of the supported harnesses. Skill names in `skills/` have no prefix; install adds one (default `_`) and renders it in the installed `SKILL.md`. Write files in `skills/`; do not invent a parallel tree.
- `README.md` is short: skill summaries, install, options. Per-skill docs go in `guide/<name>.md`.
- `docs/` is internal (criteria, references, backlog). `guide/` is user-facing.

## Language

- Everything in the repo is **English**: `README.md`, `guide/`, `docs/`, `AGENTS.md`, skills (`SKILL.md` and shipped files), changelogs, evals, code, commit messages. File names: English, kebab-case.
- Skills are **language-agnostic**: they talk to the user in the user's language and understand intent in any language. Do not hardcode Polish (or any single language) triggers or phrasings in skills.
- Structure the skills read or write (headings, field names, table columns, status values, frontmatter keys) is fixed English in every language; only free-text content follows the conversation language.

## Tests

Write tests that would fail if the promised behaviour broke, not tests that restate the code.

- Assert what a caller can observe: exit status, output, files, symlinks, backups. Do not assert that the source matches the implementation you just wrote.
- Vary every input the contract claims to read (harness, prefix, mode, skill list). A fixture must not equal a plausible hardcoded default.
- Name the invariant, then break it in your head. If a plausible bug would still pass, the test is incomplete.
- Exercise the real command; stub only external boundaries. Installer tests use a temp `HOME`, never the real one.
- Skill behaviour is checked with `skills/<name>/evals/evals.json` and the acceptance criteria, using a fresh agent. Report actual results; never claim a pass without running.

## Versioning

- One changelog for the whole project: root `CHANGELOG.md` (Keep a Changelog; package releases on top, per-skill history under "Skill history"). Every change to a skill's shipped files adds or extends an entry in the same change, under the package version and the skill's own section. A change without a changelog line is not done.
- `version` in `package.json` (SemVer) drives `update`: the installer skips a skill that is already at the current version. Bump it for every change to `skills/` or `bin/`.
- **Patch** (fix, wording, no new or removed behaviour): bump without asking.
- **Minor** (new skill or behaviour, backward compatible) and **major** (removed or changed behaviour, breaking install change): propose the level and wait for approval.
- One bump per unreleased change set: extend the current entry instead of bumping again.

## Safety

- Never write to harness dirs (`~/.claude/`, `~/.cursor/`, ...) while developing; use `--dry-run` or a temp `HOME`.
- Skills must not write secrets or personal data into files they create.
- Do not commit unless the user asks. Do not touch `.env` files.
