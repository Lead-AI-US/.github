# Lead.AI Phase 2 — CRM-lite Admin Workspace Specification
**Last Verified:** 2026-08-08  

---

## 1. CRM-LITE ROUTING & AUTHENTICATION

- **Protected Route:** `/admin/leads` and `/admin`
- **Auth Gate Component:** `AdminAuthGate.tsx`
- **Access Control:** Firebase Auth session gate / operational access key verification.
- **Unauthenticated State:** Renders secure login form. Unauthenticated deep links redirected to login.

---

## 2. DASHBOARD FEATURES

- **Operational Metrics:** Summary counts for Total Leads, New Inquiries, In Progress, and Closed/Archived.
- **Status Filter Tabs:** `All`, `New`, `Reviewed`, `Contacted`, `Qualified`, `Implementation Discussion`, `Not Ready`, `Closed`.
- **Search Filtering:** Live client-side search across Lead Name, Email, Business Name, and Requested Service.
- **Responsive Layout:** Structured data table on desktop view; responsive card list on mobile phone and tablet views.
- **Lead Detail Drawer:** Inspect contact details, service interest, challenge message, and source metadata.
- **Lead Status Management:** Dropdown updating lead status (`New` → `Reviewed` → `Qualified` → `Closed`).
- **Internal Notes & Activity History:** Add internal operational notes; view append-only activity timeline (`lead_created`, `status_changed`, `note_added`).
- **Theme System:** Seamless light/dark/system theme matching site design tokens.
