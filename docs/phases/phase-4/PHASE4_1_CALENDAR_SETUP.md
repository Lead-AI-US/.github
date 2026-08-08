# Lead.AI Phase 4.1 — Google Calendar Provider & Credential Configuration Guide
**Last Verified:** 2026-08-08

---

## 1. AUTHENTICATION ARCHITECTURE

Lead.AI uses **Google Calendar Service Account JWT authentication** (`google.auth.JWT`).
This provides direct server-to-server access to Lead.AI's consultation calendar without requiring interactive OAuth consent screens.

---

## 2. REQUIRED ENVIRONMENT VARIABLES

Configure the following environment variables in Vercel (`aruns-projects-0839d12f / lead-ai-us → Production`):

| Variable | Description | Example |
|----------|-------------|---------|
| `GOOGLE_SERVICE_ACCOUNT_EMAIL` | Service Account Client Email | `lead-ai-calendar@lead-ai-saas.iam.gserviceaccount.com` |
| `GOOGLE_SERVICE_ACCOUNT_PRIVATE_KEY` | RSA Private Key (`\n` escaped) | `"-----BEGIN PRIVATE KEY-----\nMIIEvg...` |
| `GOOGLE_CALENDAR_ID` | Lead.AI Primary Consultation Calendar ID | `c_abc1234567@group.calendar.google.com` or `primary` |
| `CRON_SECRET` | Vercel Cron Bearer Authentication Token | `<generated-32-byte-secret>` |

> [!CAUTION]
> Never expose `GOOGLE_SERVICE_ACCOUNT_PRIVATE_KEY` or `CRON_SECRET` in client-side bundles, git repositories, or frontend code.

---

## 3. GOOGLE CONSOLE SETUP STEPS

1. Go to [Google Cloud Console](https://console.cloud.google.com/).
2. Create or select project: **Lead.AI SaaS Production**.
3. Enable **Google Calendar API**.
4. Navigate to **IAM & Admin → Service Accounts** → Create Service Account `lead-ai-calendar`.
5. Create a new **JSON Key** for the Service Account and download it.
6. Open your Google Calendar app → Share the Lead.AI Consultation Calendar with `GOOGLE_SERVICE_ACCOUNT_EMAIL` giving permission **Make changes to events**.
7. Copy `client_email`, `private_key`, and `calendar_id` into Vercel production environment variables.
