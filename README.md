# project-return

A workspace for getting back up to speed after a long break (6+ months) from development.

After a pause that long, tools, models, and workflows have moved on. This repo collects what's needed to catch up: refreshed agent instructions, reusable AI skills, and research notes on project ideas worth picking back up.

## What's inside

| Path | Purpose |
| --- | --- |
| `AGENTS.md` | Agent instructions (3-layer architecture: Directives → Orchestration → Execution). Mirrored as `CLAUDE.md` / `GEMINI.md` when needed. |
| `SKILLS/` | Reusable agent skills, each with a `SKILL.md` and, where available, evals. |
| `rss/` | Research and specs for project ideas (e.g. *PolskiAI – The Case Master*). |

## Skills

- **architect**: work inside the 3-layer Directive / Orchestration / Execution pattern
- **auto-pilot**: autonomous development mode (propose, build, review, commit)
- **context-injector**: build a project context snapshot when resuming work after a break
- **dev-prompt-enhancer**: improve "build X from scratch" requests
- **research-ai-solution**: assess a pain point and whether AI can solve it (SWOT, market, business model)
- **brand-extractor**: pull brand names from a web page
- **brand-guidelines**: apply brand colors and typography
- **frontend-design**: production-grade, distinctive UI
- **gdpr-compliance**: GDPR checklist, consent banner, privacy policy
- **skill-creator**: create, evaluate, and tune skills

## Goals

1. Catch up on what changed in AI tooling and dev workflows during the pause.
2. Rebuild a reliable, repeatable workflow (directives + deterministic scripts).
3. Pick the most promising idea from `rss/` and ship it.
