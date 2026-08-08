# Lead.AI Phase 1 — Security & Compliance Notes
**Last Verified:** 2026-08-08  

---

## 1. PUBLIC CONTENT COMPLIANCE

- **Zero Pricing Rule:** Enforced across all rendered components, metadata, structured data, FAQs, and source code.
- **Zero Fake Social Proof:** All unverified logos, reviews, and adoption counters removed.
- **Responsible AI Disclaimer:** SHAP explainability notice present on Fraud Shield research section.

---

## 2. SECRETS & ENVIRONMENT

- `.env` and `.env.local` strictly ignored by Git.
- 0 API keys or private credentials exposed in client JavaScript bundles.
- Email mailto/form bridge operates client-side with consent verification.
