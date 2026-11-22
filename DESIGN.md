# General skills — design documentation

This document describes design decisions. It is not part of the skills and is not read by them at runtime. It exists to extend the set in future sessions. Every `SKILL.md` must work on its own. Acceptance criteria live in `docs/<name>-acceptance-criteria.md` and win over this document where they differ on behaviour (see `AGENTS.md`).

## 1. Scope

Skills (shipped from `skills/<name>/`, installed globally as `<prefix><name>`, default prefix `_`, e.g. `/_learnit`):

| Skill    | Purpose                                                                                                   |
|----------|-----------------------------------------------------------------------------------------------------------|
| learnit  | Guided learning of any topic in stages: scope, staged plan, teaching, per-concept checks, progress kept between sessions in `~/.claude/learning/<slug>/`. |
| mapit    | Breaks any undertaking (code, migration, move, training, event) into stages in files under `docs/plans/<slug>/`; executes stages with a gate and verification; answers plan-status questions. |
| parkit   | Parks findings from the conversation into `docs/backlog/` (`.md`, no status) for later elaboration.        |

Out of scope: trackers (Jira, ADO, Trello — tickets, sprints, grooming), plain TODO lists in the conversation, one-off "explain X" requests with no learning intent.

Hosts and harnesses: Claude Code, Cursor, Codex, OpenCode. The skills are plain Markdown instructions; no runtime code ships with them.

### General rules for all skills

- **Language-agnostic.** A skill talks to the user in the language they write in and understands intent in any language. No hardcoded triggers or phrasings in one language (no Polish-only or English-only keyword lists).
- **Fixed English structure.** Headings, frontmatter keys, field names, table columns, status values and `type` values are English in every language, used verbatim. Only free-text content follows the conversation language.
- **English file names**, kebab-case, whatever the conversation language.
- **Scoped descriptions.** The frontmatter `description` says when to invoke the skill and when not to (`Do NOT use for …`), so harnesses route requests correctly.
- **One source of truth.** Shared behaviour is referenced, not copied. Other skills are referred to by name (`_parkit`, `_mapit`), not by slash command, so the installer's prefix needs no rewriting inside bodies.
- **Ask only when needed.** `mapit` asks one question at a time with a recommendation in `interactive` mode; `autonomous` mode is used only on explicit request and records each decision marked `(autonomous)`.
- **Own data goes to the user's own locations.** `learnit` state lives in `~/.claude/learning/`, not in the working directory. `mapit` plans live in the project (`docs/plans/`). `parkit` ideas live in the project (`docs/backlog/`).
- **No secrets or personal data in created files.** Skills must not write secrets or personal data into files they create; exports (`learnit`) are checked for private data before sharing.
- **Parked ideas are not tasks.** `docs/backlog/` holds ideas, not tickets. Do not implement them "while here".

## 2. Repository layout and roles of files

```
package.json                 # name, version (SemVer), bin, files, engines (node >= 18)
bin/install.mjs              # installer, zero dependencies, built-in Node modules only
skills/<name>/SKILL.md       # the shipped skill (required)
skills/<name>/README.md      # optional
skills/<name>/evals/evals.json
skills/<name>/*.md           # support files (e.g. learnit export templates)
README.md                    # short: skill summaries, install, options
guide/<name>.md              # user-facing per-skill docs
docs/                        # internal: acceptance criteria, references, backlog
CHANGELOG.md                 # the only changelog (Keep a Changelog)
AGENTS.md                    # project rules; CLAUDE.md is a symlink to it
.gitattributes               # linguist: bin/ and *.mjs vendored, *.md counted as documentation off
```

- `skills/` is the only place for skill content. Do not invent a parallel tree.
- `docs/` is internal. `guide/` is user-facing. `README.md` stays short.
- `docs/learnit-references.md` is the research basis for `learnit`, not a source of norms.
- `docs/backlog/` holds parked ideas (`/_parkit`), not tickets.

## 3. Skill-specific design

Each skill's behaviour is defined by its `SKILL.md`; this section records only the decisions that shape the set.

### learnit
- Mode is inferred from intent (start, resume, quiz, progress, export). Invoked first whenever the user wants to learn something, even for a short definition, because the user then wants a learning program rather than an answer.
- State files have a fixed English structure (`INDEX`, `profile`, `topic`, `plan`, `knowledge`, `journal`). Reader-facing files (`lessons/`, `support/`, `exports/`) use headings in the topic language.
- Export produces a recipient package: a fixed template for instructions (`export-readme.md`) and a fixed tutor prompt (`export-tutor-prompt.md`), copied in full rather than composed anew, because composing them dropped the style rules.
- Migration of older topic files converts on first write, maps content 1:1, never drops content, keeps unmapped sections at the end and notes it in the journal.

### mapit
- Three phases: plan, execution, query. Plan files under `docs/plans/<slug>/`; statuses and `Planning: draft|complete` are fixed English.
- Execution runs each stage with a gate and verification. Plans may start from an idea in `docs/backlog/` created by `_parkit`.

### parkit
- Only when invoked by the user; never suggests saving on its own.
- Items have no status: a scratchpad for later elaboration. Frontmatter keys, section headings and `type` values are fixed English.
- Nothing to park → say so; no invented content.

## 4. Installer (`general-skills`)

### Invocations

- `npx general-skills install` (npm), `npx github:<owner>/<repo> install` (git), `node bin/install.mjs <cmd>` (local clone).
- Subcommands: `install`, `update`, `uninstall`, `list`.
- Options: `--harness claude,cursor,codex,opencode` (default: detected), `--skills learnit,mapit` (default: all, source names without prefix), `--prefix P` (default `_`; installed name = prefix + source name; `""` for none; allowed characters: letters, digits, `_`, `-`), `--mode copy|symlink` (default `copy`), `--dry-run`, `--force`, `-h|--help`.

### Target directories

| Harness     | Global directory                                  | Override                         |
|-------------|---------------------------------------------------|----------------------------------|
| Claude Code | `~/.claude/skills/`                               | `CLAUDE_CONFIG_DIR`              |
| Cursor      | `~/.cursor/skills/`                               | none                             |
| Codex       | `~/.agents/skills/`                               | `CODEX_HOME` (older `~/.codex/skills/`) |
| OpenCode    | `~/.config/opencode/skills/`                      | `XDG_CONFIG_HOME`                |

Harness detection: the harness config directory exists. Not detecting a harness is not an error; the user passes `--harness`.

### Rules

- **Ownership marker.** Each installed directory contains `.general-skills.json` (`package`, `version`, `mode`, `installedAt`). The installer overwrites and removes only directories it owns: a marker with its package name, or, in symlink mode, a symlink pointing into the package.
- **Foreign skills.** A directory without a marker (a user skill with the same name) is skipped with a message. `--force` moves it to `*.bak` and installs.
- **Idempotence.** Reinstalling the same version and mode changes nothing (`= up to date`).
- **Modes.** `copy` copies the skill. `symlink` writes a rendered `SKILL.md` (the frontmatter `name` must equal the installed name, because it becomes the slash command) and symlinks the other files to the clone.
- **Cursor duplicates.** Cursor also reads `~/.claude/skills/`, `~/.agents/skills/` (and `~/.codex/skills/`). When Cursor is selected alongside a harness it already sees, `~/.cursor/skills/` is skipped with a message; `--harness cursor` forces it.
- **Old names.** The installer never removes skills under old names. `LEGACY` in `bin/install.mjs` is reserved for warnings about them; it is empty at 0.2.0.
- **`--dry-run`** prints the plan (source → destination) and writes nothing.
- **No network, no dependencies, no `postinstall`.** Installation is explicit: skills change how the agent behaves, so the user adds them deliberately. Nothing is written outside the package at install time.

### Tests

- Installer tests use a temp `HOME` (and temp `CLAUDE_CONFIG_DIR`/`XDG_CONFIG_HOME`/`CODEX_HOME` where relevant), never the real one. Never write to harness directories (`~/.claude/`, `~/.cursor/`, …) while developing; use `--dry-run` or a temp `HOME`.
- Tests exercise the real command and assert observable results: exit status, output, files, symlinks, backups. They vary harness, prefix, mode and skill list; a fixture must not equal a plausible default.
- Skill behaviour is checked with `skills/<name>/evals/evals.json` and the acceptance criteria, using a fresh agent. Results are reported as they actually ran.

## 5. Versioning, changelog and releases

- `version` in `package.json` is SemVer and drives `update`: the installer skips a skill already at the current version. Bump it for every change to `skills/` or `bin/`. A change without a bump never reaches installed copies.
- **Patch** (fix, wording, no new or removed behaviour): bump without asking.
- **Minor** (new skill or backward-compatible behaviour) and **major** (removed or changed behaviour, breaking install change): propose the level and wait for approval.
- One bump per unreleased change set: extend the current entry instead of bumping again.
- One changelog: root `CHANGELOG.md`. Package releases on top; per-skill history under "Skill history". Every change to a skill's shipped files adds or extends an entry in the same change. A change without a changelog line is not done.
- Git tags `vX.Y.Z` mark releases. Tag existence is not verified in this document; check `git tag` before a release.

## 6. Decision log

Dated entries, taken from `CHANGELOG.md`. A changed rule gets a new entry; old entries are not edited silently.

- **2026-11-21** — Package 0.1.0: initial release (`install`, `update`, `uninstall`, `list`).
- **2026-11-21** — Package 0.2.0: repository docs (`README.md`, `guide/`, `AGENTS.md`, single `CHANGELOG.md`); all skill content, docs and evals translated to English; skills made language-agnostic with fixed English structure.
- **2026-11-21** — `learnit` 0.5.1: canonical English headings and columns per state file; migration of older files converts on first write and never drops content. Reason: a conversion silently dropped a section and mixed languages in headings.
- **2026-11-21** — `learnit` export uses fixed templates (`export-readme.md`, `export-tutor-prompt.md`) copied in full. Reason: composed prompts lost the style rules.
- **2026-11-21** — Acceptance criteria are the completion standard: verification runs in one pass, at most two fix passes, new edge cases go to `docs/backlog/` instead of the skill.

## 7. Open points

- Verify harness paths (section 4) against current installed versions of each harness before a release. Cursor, Codex and OpenCode paths were taken from documentation, and OpenCode from third-party sources — unverified in this repository.
- Behaviour of Claude Code–specific frontmatter fields in other harnesses is assumed to be ignored when unknown (unverified). If a harness rejects them, the installer would have to generate simplified frontmatter.
- Release tagging (`vX.Y.Z`) and the `update` path against a real older install are not verified in this repository.

## 8. Extending

- **New skill:** add it to section 1 with its purpose and out-of-scope list; apply the general rules in section 1; add `skills/<name>/SKILL.md`, `evals/evals.json`, acceptance criteria in `docs/`, a `guide/<name>.md` page, and a changelog entry.
- **New harness:** add it to the `HARNESS` table in `bin/install.mjs`, to section 4, and log the decision.
- **New installer option or subcommand:** document it in section 4 and `README.md`, and log it.
- **README.md and guide/:** keep in sync with skill behaviour, flags and installer options.
- **Changing a rule:** add a new decision-log entry with the date and reason; do not edit the old rule silently.
- **Ideas that come up while building a skill:** park them in `docs/backlog/` with `_parkit`; do not implement them as part of the current change.
