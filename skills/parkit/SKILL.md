---
name: parkit
description: Parks findings from the conversation (a feature, fix, optimization, idea) into an in-repo scratchpad of ideas (docs/backlog/, .md files) for later elaboration. Use for park this, save for later, set this aside, in any language. Also use to review parked ideas, return to one, change it, or delete it. Do NOT use for a backlog in Jira/Trello/another tracker (tickets, sprints, grooming). Recognise intent, not words.
---

# _parkit

Saves ideas worked out in the conversation to `.md` files in `docs/backlog/`. It is a scratchpad for later elaboration: items have no status. The skill is language-agnostic: talk to the user in their language and understand their intent in any language. Structure (frontmatter keys, section headings, `type` values) is fixed English; content is in the conversation language; file names are English.

## When it acts

Only when invoked by the user; it never suggests saving on its own. A bare invocation with no hint = park the findings from the conversation. Nothing to park → say so, don't invent content. Infer intent from what the user says (no commands); unclear → ask in one sentence.

## Intents

- **Park**: extract the findings from the conversation, show a preview, save after approval.
- **Review**: a table (date, type, title, file), newest on top; the user may narrow by kind or topic. An entry "moved to plan <slug>" in "History" → append `→ plan <slug>` to the title. No directory → "nothing parked", create nothing.
- **Return**: find the file by description (several match → ask), load it, summarise briefly; check that `path:line` references are current before use. Don't change the file. Breaking it into stages is `_mapit`'s job.
- **Change or delete**: editing or deleting a file in `docs/backlog/` needs a preview and explicit confirmation. An edit adds an entry to "History".

## Location

`docs/backlog/` at the repo root, not in the current subdirectory.

1. Walk up from the working directory looking for `docs/backlog/`, then `docs/`; stop at a directory with `.git` (directory or file) or the filesystem root.
2. One place → use it (create `backlog/` if missing). Several → ask.
3. None → ask where to create it; propose the repo root. Create nothing without confirmation.
4. Only `docs/`, not `doc/`.

## What to save

- Only what was settled or explicitly discussed. One topic = one file.
- `type`: `feature` | `fix` | `optimization` | `idea`.
- List gaps under "Open questions"; don't ask about every detail.

## Sanitisation

Don't save: secrets (passwords, tokens, keys, connection strings), personal data (people, e-mails, phones, clients), internal URLs and hosts. Replace with a description or placeholder (`<token>`, "client X"); when the idea loses meaning, skip it and note it under "Open questions". This applies to the file name, `source`, and `tags` too. Mark in the preview what was anonymised.

## Preview before saving

Before creating or changing a file, show it and wait for approval (even for a single item):

| # | Title | type | File | Content (1 line) |
|---|-------|------|------|------------------|

State the target directory, deduplication, and sanitisation. The user may merge, split, or remove items, or change titles, types, and names.

## File name

English, lowercase, `-`, 3–6 words, max 50 characters, e.g. `cache-for-report-queries.md`. Name taken by another topic → suffix `-2`.

## Deduplication

Before the preview look for a similar idea (title, tags, content, meaning). Found → show it and ask: append or new file. Appending: fit into matching sections without repetition, and add an entry to "History".

## File format

```markdown
---
title: <short title>
type: feature | fix | optimization | idea
date: YYYY-MM-DD
source: <summary of the conversation context, one line>
tags: [<optional>]
---

## Context
## Problem / goal
## Proposed solution
## Rejected alternatives
## Acceptance criteria
## Open questions
## Risks
## Related files
- `path/to/file.ext:42`: why it matters
## History
- YYYY-MM-DD: created
```

Omit sections with no coverage in the conversation (except "History"). "Context": one sentence on why it was parked (e.g. awaiting a decision, too big for now), if it follows from the conversation. "History": always last; on creation an entry "created", on each change or append one line with the date and what changed. Each section up to ~4 lines, the file usually under ~40 lines; a long conversation → several files. Content in the conversation language, file name in English. `date` from the environment context or `date +%F`, never estimated. Quote YAML values with special characters (e.g. `:`, `#`). "Related files": paths from the project root, don't guess.

Example (`cache-for-report-queries.md`):

```markdown
---
title: "Cache: report queries to an external API"
type: optimization
date: 2026-11-16
source: conversation about slow loading of the reports dashboard
tags: [api, performance]
---

## Context
Parked: the cache location has to be decided first.

## Problem / goal
The dashboard queries the API about 12 times per refresh. Shorten loading.

## Proposed solution
- Cache results, TTL 5 min, key = endpoint + parameters.

## Open questions
- In-process memory or Redis?

## History
- 2026-11-16: created
```

## Rules

- No git operations or commits.
- Don't modify files outside `docs/backlog/`; don't create `docs/` without confirmation.
- Don't save or delete without confirming the preview.
- After saving, give the full paths of the changed files.
