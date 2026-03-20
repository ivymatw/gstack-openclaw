# gstack-openclaw

A port of [Garry Tan's GStack](https://github.com/garrytan/gstack) skill pack into [OpenClaw](https://openclaw.io) — translated from a code-sprint tool into a conversational decision-making framework.

## What This Is

GStack's real value isn't code automation — it's **structured thinking**. The six YC forcing questions don't require a codebase. The Iron Law of debugging applies to any problem. The CEO review instinct ("find the 10-star product hiding inside this request") is pure decision-making discipline.

This port preserves those frameworks completely and adapts the mechanics for conversational use.

## The Five Ported Skills

| Skill | Framework | Use When |
|---|---|---|
| `office-hours` | YC's 6 forcing questions | You have an idea and need to think it through |
| `ceo-review` | Brian Chesky's 10-star thinking + 18 CEO patterns | You have a plan and need strategic challenge |
| `investigate` | Iron Law: no fixes without root cause | Something isn't working and you don't know why |
| `eng-review` | Architecture diagrams + failure mode mapping | You have a technical design that needs review |
| `retro` | Weekly retrospective + trend analysis | End of week reflection on projects and goals |

## Key Differences from GStack

| GStack | This Port |
|---|---|
| Coding loop (Idea → Code → Ship) | Decision loop (Problem → Decision → Action) |
| File system artifacts (`~/.gstack/projects/`) | Obsidian notes (`obsidian/GStack/`) |
| AskUserQuestion tool calls | Natural conversational questions |
| YC application pitch | Removed (not relevant to target user) |
| Bash preamble + telemetry | Removed |
| Works in active coding sessions | Works in idea exploration + decision-making |

## Design Documents

- **[SPEC.md](SPEC.md)** — Why this port exists and the philosophical foundation
- **[DESIGN.md](DESIGN.md)** — Exhaustive framework documentation (source of truth — read this to understand everything)
- **[PROMPTS.md](PROMPTS.md)** — Production-ready SKILL.md content for all 5 skills

## Skills

```
skills/
  office-hours/SKILL.md
  ceo-review/SKILL.md
  investigate/SKILL.md
  eng-review/SKILL.md
  retro/SKILL.md
```

## Based On

[GStack](https://github.com/garrytan/gstack) by Garry Tan, MIT License.
