---
name: gdpr-compliance
description: Makes a project compliant with GDPR (General Data Protection Regulation) requirements. Use this skill whenever the user mentions GDPR, privacy laws, data protection, cookie consent, user data deletion, right to be forgotten, data subject rights, personally identifiable information (PII), privacy policy, data processing agreements, or user consent. Also trigger when the user wants to deploy an app to EU users, or asks about privacy regulations, legal compliance, or data handling. This skill covers the full spectrum of GDPR compliance: frontend consent UI, backend data handling, cookie policies, privacy APIs, and audit checklists.
---

# GDPR Compliance Skill

This skill helps you make a web application compliant with the EU General Data Protection Regulation (GDPR). Compliance is a multi-layer concern covering the **frontend** (user consent & transparency), the **backend** (data handling, storage, & deletion), and **legal documents** (Privacy Policy, Cookie Policy).

## Step 1: Audit the Project

Before making any changes, survey the codebase to understand the current state. Look for:

- **Tracking scripts** — any analytics, session recording, or pixel-based tracking (e.g. Facebook Pixel, Google Analytics)
- **User data collection** — forms, accounts, email capture, event tracking, purchase data
- **Database tables** — identify which tables store personally identifiable information (PII): names, emails, IPs, cookies, device IDs, session tokens
- **Third-party services** — any integrations that receive user data (e.g. payment processors, email providers, AI APIs)
- **Cookies and localStorage** — what is being set and why

Once you have a clear picture, refer to the `references/gdpr-checklist.md` file for a full checklist of what is required.

## Step 2: Implement Consent Management

GDPR requires that users give **informed, specific, freely given, and unambiguous consent** before any non-essential data processing begins (including analytics tracking).

**What to build:**
1. A **Cookie Consent Banner** on the frontend that:
   - Is shown on first visit to any page
   - Explains what data is collected and why
   - Has an "Accept All", "Reject Non-Essential", and optionally "Manage Preferences" option
   - Does NOT pre-tick optional categories
   - Remembers the user's choice (stored in a first-party cookie `gdpr_consent`)
   - Links to the full Cookie/Privacy Policy page
2. **Conditional script loading** — tracking scripts (like your `/tracker.js`) should only load and fire events **after** the user has accepted analytics/tracking consent.

See `references/consent-banner.md` for an implementation example and code template.

## Step 3: Protect Personal Data on the Backend

GDPR requires that you handle personal data lawfully, fairly, and securely.

**Key backend requirements:**

- **Minimize data collected** — only store what is strictly necessary
- **Anonymize where possible** — e.g., truncate IP addresses, avoid storing full referrer URLs if not needed
- **Set data retention limits** — delete event/tracking data older than a defined period (e.g. 12 months)
- **Encrypt sensitive fields** — user passwords must be hashed (not stored in plain text). Emails may also need encryption at rest depending on regulatory context.

> [!CAUTION]
> Your current server.ts stores **passwords in plain text** in the database. This is a GDPR (and security) violation. Passwords must be hashed using a secure algorithm like **bcrypt** before storage.

**Add an API for Data Subject Rights:**

GDPR grants users specific rights. You must implement:

| Right | API Endpoint to create |
|---|---|
| Right of Access | `GET /api/user/data-export` — returns all data held on the user |
| Right to Erasure | `DELETE /api/user/data-delete` — permanently deletes all PII for the user |
| Right to Portability | `GET /api/user/data-export` (same as above, return JSON format) |

## Step 4: Implement a Privacy Policy & Cookie Policy

Your app must have publicly accessible legal documents that explain:
- What data you collect and why
- Who you share it with (list all third parties: Supabase, Google Gemini API, etc.)
- How long you retain data
- How users can exercise their rights (contact email or form)
- That you use cookies and what each cookie does

Create a `/privacy` route in your React app with this content. See `references/privacy-policy-template.md` for a starting template you can customize.

## Step 5: Secure API Endpoints

- Add **rate limiting** to auth endpoints (`/api/auth/register`, `/api/auth/login`) to prevent brute force attacks
- Ensure API endpoints that return user data (`/api/websites`, `/api/user/data-export`) validate that the authenticated user only sees their own data — no user ID should be accepted from the client without server-side verification

## Step 6: Verify with the Compliance Checklist

After implementing changes, go through `references/gdpr-checklist.md` line by line and mark each item as complete. Present the final checklist to the user.

---

## What to do when this skill is invoked

1. **Audit first** — scan the project and summarize findings before touching anything
2. **Prioritize critical issues** — flag the password hashing issue and missing consent banner immediately
3. **Implement in order** — Consent → Data handling → APIs → Legal pages → Checklist
4. **Don't break existing features** — wrap consent-gating around tracking scripts rather than removing them
5. **Explain trade-offs** — some compliance steps (like bcrypt for passwords) require new npm packages; inform the user

Read the reference files as needed:
- `references/gdpr-checklist.md` — Full compliance checklist
- `references/consent-banner.md` — Cookie consent banner implementation guide
- `references/privacy-policy-template.md` — Privacy Policy starting template
