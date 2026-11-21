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

### With npx

```bash
npx github:meehow-halas/general-skills install
```

### From GitHub (clone)

```bash
git clone https://github.com/meehow-halas/general-skills.git
```

```bash
cd general-skills && node bin/install.mjs install
```

## Options

```bash
npx github:meehow-halas/general-skills install --harness claude --skills learnit,mapit --dry-run
```

| Option | Meaning |
|---|---|
| `--harness a,b` | `claude,cursor,codex,opencode` (default: detected) |
| `--skills a,b` | selected skills (default: all) |
| `--prefix P` | name prefix, default `_`; `""` for none |
| `--mode M` | `copy` (default) or `symlink` |
| `--dry-run` | print the plan, change nothing |
| `--force` | overwrite unmanaged dirs (backup `*.bak`) |

Other commands: `update`, `uninstall`, `list`.

## License

MIT
