# Context Snapshot Template

This is the canonical output format for the `context-injector` skill.
Save the output to `directives/context_snapshot.md` each time it runs.

---

```markdown
# 📍 Project Context Snapshot — [Project Name]
Generated: [YYYY-MM-DD HH:MM] ([timezone])

## 🧭 Project Identity
- **What it is**: [1-2 sentences]
- **Stack**: [Languages, frameworks, DB, hosting]
- **Deployment**: [Where and how it runs]

## ✅ Completed Milestones
| Sprint/Phase | What Was Delivered |
|---|---|
| Sprint 1 | [e.g., Core tracking pipeline, Supabase integration, real-time dashboard] |
| Phase 2 | [e.g., Funnel analysis, AI Insights tab, one-page vs multi-stage auto-detection] |

## 🔄 Current Sprint / Phase
- **Sprint**: [e.g., Sprint 2 — Phase 3: Behavioral & Financial Depth]
- **In Progress**:
  - [ ] [Task 1]
  - [ ] [Task 2]
- **Blocked / Needs Attention**:
  - [?] [Any blockers, or "None"]

## 🔑 Key Architecture Decisions
- [Decision 1]
- [Decision 2]

## 📡 Live API Surface
| Method | Route | Description |
|---|---|---|
| POST | /api/events | Receives tracking events from tracker.js |
| GET | /api/websites/:id/stats | Returns session, conversion, bounce metrics |
| GET | /api/websites/:id/funnel | Returns funnel step counts |
| POST | /api/websites/:id/insights | Triggers Gemini AI analysis |
| GET | /api/websites/:id/insights | Returns saved AI insights |

## 🛢️ Database Schema (live tables)
| Table | Key Columns |
|---|---|
| `users` | id, email, password |
| `websites` | id, user_id, name, domain, tracking_id, type, reset_scheduled_at |
| `events` | id, tracking_id, event_name, timestamp, session_id, user_id, page_url, referrer, device_type, properties (JSONB) |
| `insights` | id, website_id, content, created_at |

## 🎯 Tracked Events
| Event | When It Fires | Significance |
|---|---|---|
| `page_view` | On page load | Passive — not engagement |
| `discovery_product` | Product/price enters viewport | Passive — not engagement |
| `click` | Button/link clicked | Active engagement |
| `intent_add_to_cart` | Cart-related click detected | High intent |
| `intent_checkout` | Checkout-related click detected | High intent |
| `checkout_start` | First form field interaction | Checkout funnel entry |
| `checkout_progress` | Each identified form field filled | Funnel depth |
| `purchase` | Form submitted with checkout context | Conversion |

## 🚀 Next Up (immediately actionable)
- [ ] [Next task — specific enough to start immediately]
- [ ] [Next task 2]

## ⚠️ Known Issues / Gotchas
- [Issue 1 — or "None"]
```
