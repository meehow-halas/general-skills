# general-skills

General-purpose skills for AI agents (Claude Code, Cursor, Codex, OpenCode). Installed as `/_learnit`, `/_mapit`, `/_parkit`.

## Skills

### [_learnit](guide/learnit.md)
Learning mentor for any topic: staged plan, lessons, knowledge checks, spaced repetition, progress remembered across sessions.

### [_mapit](guide/mapit.md)
Breaks any undertaking into stages in `docs/plans/<slug>/`, executes them with a gate and verification, answers questions about plan status.

### [_parkit](guide/parkit.md)
Parks ideas from a conversation in `docs/backlog/` as `.md` files; review, revisit, edit. Feeds `_mapit`.

## Install

Requires Node ≥ 18. Installs into detected harnesses by default.

Directly from GitHub, no clone needed:

```bash
npx github:meehow-halas/general-skills install
```

Run with `--dry-run` first to see the plan without writing anything.

## Options

| Option | Meaning |
|---|---|
| `--harness a,b` | `claude,cursor,codex,opencode` (default: detected) |
| `--skills a,b` | selected skills (default: all) |
| `--prefix P` | name prefix, default `_`; `""` for none |
| `--mode M` | `copy` (default) or `symlink` |
| `--dry-run` | print the plan, change nothing |
| `--force` | overwrite unmanaged dirs (backup `*.bak`) |

Other commands: `update`, `uninstall`, `list`.

Examples:

```bash
npx github:meehow-halas/general-skills install --dry-run
npx github:meehow-halas/general-skills install --harness claude,codex --skills learnit,mapit
npx github:meehow-halas/general-skills install --prefix my_
npx github:meehow-halas/general-skills update
npx github:meehow-halas/general-skills list
npx github:meehow-halas/general-skills uninstall --harness cursor
```

## License

MIT
