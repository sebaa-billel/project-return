---
name: context-injector
description: Generates and injects a rich project context snapshot to keep the model grounded, relevant, and consistent — especially when the conversation history is long, a new session is starting, or a new sprint is kicking off. Use this skill whenever: (1) the user starts a new chat or session, (2) a new sprint or phase is beginning, (3) relevant past work (features, decisions, bugs) seems to be getting lost, (4) the user says things like "remind yourself", "where were we", "start of sprint", "new session", or "catch up". Always prefer this skill when resuming work after a break or switching between major features. The context snapshot should be injected automatically — don't wait to be asked.
---

# Context Injector Skill

This skill maintains **project continuity and context health** across sessions, context window resets, and sprint boundaries. Its job is to produce a structured, concise snapshot of the project that can be injected back into the model's context — keeping the AI grounded in what the project is, what has been done, what's in progress, and what's next.

Think of it as a "smart resume" that the agent generates and reads back to itself.

---

## When to Trigger

Trigger this skill automatically in any of these situations:

1. **New session / conversation start** — When the user is starting fresh and recent decisions or code are not in context.
2. **New sprint / phase boundary** — When transitioning between sprints (e.g., Sprint 1 → Sprint 2) or phases (e.g., Phase 2 → Phase 3).
3. **Context drift** — When the conversation has grown long and the model seems to be forgetting recent decisions, architecture choices, or prior work.
4. **Explicit "catch me up" request** — When the user says "where were we", "what did we do last time", "remind yourself", "new chat", etc.

---

## How to Generate the Context Snapshot

When triggered, gather context from the sources in this order (read as many as are relevant):

### Step 1: Read Directives
Read all files in `directives/*.md`. These define the project's rules, SOP, and key definitions. They are the ground truth for how the project should operate.

### Step 2: Read the Roadmap
Check for any roadmap or sprint planning documents (look in the brain/artifact directories, or ask the user if none are obvious). Extract:
- Current sprint / phase number
- Completed milestones
- In-progress items
- Upcoming / next items

### Step 3: Inventory the Codebase State
Scan key source files to understand what exists. Focus on:
- `server.ts` (or equivalent backend) — What API endpoints exist? What DB tables are live?
- `src/pages/` — What dashboard pages/views are implemented?
- `src/components/` — What UI components exist?
- `tracker.js` (if applicable) — What events are being tracked?
- Any `execution/` scripts or config files

Do **not** read every file verbatim — skim for structure and note what's there.

### Step 4: Read Recent Insights (if any)
Check `skills/*/evals/` or any insight/analysis files for recent AI-generated findings that should inform the current sprint.

### Step 5: Identify Open Items
Look for any `TODO`, `FIXME`, or open task markers in the codebase, plus any items marked `[ ]` in task.md or roadmap documents.

---

## Output Format: The Context Snapshot

After gathering, produce the snapshot in this exact format. Keep it dense but readable — this is meant to be consumed by the model, not just the user.

```
# 📍 Project Context Snapshot — [Project Name]
Generated: [timestamp]

## 🧭 Project Identity
- **What it is**: [1-2 sentence summary of the product/system]
- **Stack**: [e.g., Express + TypeScript backend, React frontend, Supabase/Postgres, Vercel]
- **Deployment**: [e.g., Vercel serverless, local dev on port 3000]

## ✅ Completed Milestones
- [Sprint/Phase]: [What was delivered — be specific about features]
- ...

## 🔄 Current Sprint / Phase
- **Sprint**: [e.g., Sprint 2 — Phase 3]
- **In Progress**:
  - [Task 1]
  - [Task 2]
- **Blocked / Needs Attention**:
  - [Any known blockers or issues]

## 🔑 Key Architecture Decisions
- [Decision 1 — e.g., "Funnel type (one-page vs multi-stage) is auto-inferred from events"]
- [Decision 2 — e.g., "Tracker.js is served dynamically from the backend, not bundled"]
- ...

## 📡 Live API Surface
- [METHOD] /api/[route] — [what it does]
- ...

## 🛢️ Database Schema (live tables)
- `[table_name]`: [key columns]
- ...

## 🎯 Tracked Events
- `[event_name]`: [when it fires and why it matters]
- ...

## 🚀 Next Up (immediately actionable)
- [Next task 1 — with enough detail to start work immediately]
- [Next task 2]
- ...

## ⚠️ Known Issues / Gotchas
- [Issue 1 — e.g., "CORS is permissive for now, needs tightening in production"]
- ...
```

---

## Instructions for Injection

After generating the snapshot:

1. **Save the snapshot** to `directives/context_snapshot.md` (overwrite every time — it should always reflect current state).
2. **Announce it** to the user: "🧠 Context loaded. Here's where we are: [paste the snapshot inline in the chat]"
3. **Use it going forward** as your working memory reference. When making decisions, check it for consistency with the architecture, existing APIs, and in-progress work.

---

## Quality Rules

- **Be specific over generic.** "Phase 3: Behavioral Depth" is better than "we're working on analytics".
- **Timestamps matter.** Always include when the snapshot was generated so you and the user can tell if it's stale.
- **Don't pad.** If a section has no content (e.g., no known issues), write "None" rather than leaving it empty or making things up.
- **Conciseness beats completeness.** A dense 1-page snapshot is more useful than a vague 5-page one.
- **When in doubt, flag it.** If you're unsure about a fact (e.g., whether a feature is done or not), mark it with `[?]` so the user can correct it.

---

## Triggering on New Sprint / Session

When the user signals a new sprint or session is starting:
1. Run through all 5 gathering steps above.
2. Generate the snapshot.
3. Save to `directives/context_snapshot.md`.
4. Present it to the user and ask: "Does this capture where we are? Any corrections before we dive in?"

This creates a shared baseline that both you and the user agree on — reducing drift and keeping collaboration tight.
