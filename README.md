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
2. Rebuild a reliable, repeatable workflow (directives + deterministic scripts), with this repo as the single source for shared skills.
3. Get every paused project back to a running, secure state, then focus on the one with the clearest path to revenue.
4. Pick the most promising idea from `rss/` and decide whether to start it.

## Paused projects

All are private repos under `sebaa-billel`. Each one's state is as of its last commit.

| Project | What it is | Stack | Last active | Where it stopped |
| --- | --- | --- | --- | --- |
| [conversion-recover-agent](https://github.com/sebaa-billel/conversion-recover-agent) | E-commerce behavioral analytics with zero-integration `tracker.js` and AI recovery suggestions | React/Vite, Express (TS), Supabase, Gemini 2.5 Flash, Vercel | 2026-04-10 | Phase 1 refactor done. **Phase 2 (real auth) not started.** Auth is still fake: plaintext passwords and `userId` passed in query params, on a live deployment. |
| [archdraft-ai-gen](https://github.com/sebaa-billel/archdraft-ai-gen) | Turns a *cahier de charge* (PDF/DOCX) into an architectural program, 2D floor plan and DXF | Next.js 16, Tailwind v4, Supabase, Gemini/Claude | 2026-03-24 | Layout engine v9 (6 sub-engines). Placements are still unreliable, and DXF export is only a placeholder (Phase 3). |
| [ecom-landingpage-alani9](https://github.com/sebaa-billel/ecom-landingpage-alani9) | Localized (AR/FR/EN) landing page and admin dashboard for an Algerian e-commerce store | React/Vite, Firebase, Gemini, Vercel | 2026-03-16 | Feature-complete. Last commits added a tracking script plus debug toasts "for testing", which are still in. |
| [order-entry-ai-agent](https://github.com/sebaa-billel/order-entry-ai-agent) ("Aegis") | Autonomous order-entry agent: CRM case → CPQ corrections → SAP S/4HANA payload | Python/FastAPI, mock Salesforce/CPQ/SAP APIs | 2026-03-07 | Phase 1 MVP done through SAP step 1 (VA21). Steps 2–3 (VA41 contract, order conversion) and Phase 2 multi-tenant SaaS not started. |

## Sprints

Sprints are about one week each. Check boxes as work lands.

### Sprint 0: Re-onboarding (all projects)
- [ ] Clone all four repos locally and get each one running (`npm install` / `pip install`, `.env` from the templates)
- [ ] Check external services are still alive: Vercel deployments, Supabase projects (free-tier projects pause after inactivity), Firebase, API keys
- [ ] Rotate API keys and secrets that sat unused for 6+ months
- [ ] Update dependencies and LLM models to current versions (several repos still pin Gemini 2.0/2.5 Flash)
- [ ] Remove committed artifacts (`analytics.db*` in conversion-recover-agent)
- [ ] Make `project-return/SKILLS` the single source for shared skills (currently copied into every repo) and note in each repo how it pulls them in

### Sprint 1: conversion-recover-agent, real auth (security first)
- [ ] Supabase Auth for signup/login/logout and removal of plaintext passwords
- [ ] JWT middleware (`getUser()`) on every `/api/*` route, with no `userId` in query params
- [ ] Frontend protected routes (`useAuth`) and rate limiting on auth endpoints
- [ ] Re-test the tracker on a live page (ecom-landingpage-alani9 is a natural first test site)

### Sprint 2: conversion-recover-agent, onboarding and billing groundwork
- [ ] Welcome wizard, empty states and demo-data mode (roadmap Phase 3)
- [ ] Draft pricing and LLM cost model, then pick a payment provider (roadmap Phase 4)

### Sprint 3: archdraft-ai-gen, make the layout reliable
- [ ] Build a small set of real *cahier de charge* test cases with expected layouts
- [ ] Fix circulation, adjacency and floating-room issues against those cases
- [ ] First working DXF export with `ezdxf` or an equivalent (walls, labels, layers)

### Sprint 4: order-entry-ai-agent, finish the SAP flow
- [ ] SAP step 2: conditional contract creation (VA41)
- [ ] SAP step 3: order conversion (ZSD_OMW)
- [ ] Decide whether Phase 2 (multi-tenant SaaS) is worth pursuing or the project stays a portfolio/demo piece

### Sprint 5: Review and focus
- [ ] Compare the projects on traction, effort left and revenue potential
- [ ] Choose one main project for the next quarter and park the rest with a clean README and status
- [ ] Revisit the `rss/` ideas (PolskiAI) against that choice

**Ongoing:** ecom-landingpage-alani9 gets maintenance only (remove the debug toasts, confirm the tracking script and Meta Pixel work).
