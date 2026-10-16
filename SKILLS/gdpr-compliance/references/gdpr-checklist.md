# GDPR Compliance Checklist

Use this checklist after implementing GDPR changes. Mark each item `[x]` when complete.

---

## 🍪 Consent & Cookies

- [ ] Cookie consent banner shown on first visit to new users
- [ ] Banner has: "Accept All", "Reject Non-Essential" (and optionally "Manage Preferences")
- [ ] No non-essential cookies or tracking scripts load before consent is given
- [ ] Consent choice is remembered (stored in `gdpr_consent` first-party cookie)
- [ ] Cookie consent can be withdrawn (link in the footer to manage preferences)
- [ ] Cookie policy lists every cookie used, its purpose, and its lifetime

---

## 📋 Privacy Policy

- [ ] A publicly accessible `/privacy` page exists
- [ ] Policy identifies the data controller (your business name + contact)
- [ ] Policy lists all data collected (name, email, IP, device type, events, etc.)
- [ ] Policy explains the **legal basis** for each type of processing (Consent, Legitimate Interest, Contract, etc.)
- [ ] Policy names all **third-party sub-processors** (e.g. Supabase, Google Gemini, Vercel)
- [ ] Policy states the data **retention period** for each data category
- [ ] Policy explains how users can exercise their rights (see below)
- [ ] Policy is written in plain, understandable language

---

## 🔐 Data Security

- [ ] Passwords are **hashed** using bcrypt or Argon2 (NOT stored as plaintext)
- [ ] Database connections use SSL/TLS (Supabase does this by default)
- [ ] API endpoints are protected from brute force attacks (rate limiting on `/api/auth/*`)
- [ ] Users can only access their own data (server-side user ID validation — never trust client-provided user IDs without authentication)
- [ ] Sensitive data at rest is encrypted where applicable (e.g. Supabase encryption at rest)

---

## 🧑 Data Subject Rights (User Rights)

- [ ] **Right of Access**: `GET /api/user/data-export` — Provides a full export of all data held about the user
- [ ] **Right to Erasure**: `DELETE /api/user/data-delete` — Permanently deletes all user PII
- [ ] **Right to Portability**: Data export is in a machine-readable format (JSON)
- [ ] Instructions for exercising rights are listed in the Privacy Policy
- [ ] Response time for rights requests: no more than **30 days** from request

---

## 📉 Data Minimization & Retention

- [ ] Only data that is strictly necessary for the service is collected
- [ ] Anonymous or aggregate data is preferred where individual tracking isn't needed
- [ ] A data retention policy is set (e.g. tracking events deleted after 12 months)
- [ ] Old data is actually deleted (a scheduled job or periodic manual cleanup)
- [ ] IP addresses logged (if at all) are truncated (e.g. `192.168.1.x`)

---

## 📝 Tracking & Analytics

- [ ] The tracking script (`/tracker.js`) only loads **after** cookie consent is given
- [ ] Users who reject tracking are not tracked at all
- [ ] Tracking IDs are pseudonymous (random identifiers, not directly tied to email)
- [ ] Users can revoke consent and have their tracking history deleted

---

## 🌍 Third-Party Integrations

- [ ] **Supabase** — Data Processing Agreement (DPA) reviewed and accepted via Supabase dashboard
- [ ] **Google Gemini API** — Data not sent to Gemini for training purposes; reviewed Google's AI data usage terms
- [ ] **Vercel** — Vercel's DPA reviewed; region of data processing noted (EU regions preferred for EU users)
- [ ] Any other third-party listed in the privacy policy with a link to their own privacy policy
