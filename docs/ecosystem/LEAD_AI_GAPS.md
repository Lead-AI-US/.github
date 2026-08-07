# Lead.AI Gaps Analysis
**Phase 0.5 Baseline**  
**Last Verified:** 2026-08-07  

---

## TIER 1 — CONTROL-PLANE & DOMAIN ALIGNMENT

### G-001: Apex Domain Project Routing
- **Status:** PENDING DASHBOARD ALIAS TRANSFER
- **Finding:** `lead-ai-us.vercel.app` (the project under approved team `aruns-projects-0839d12f`) is fully verified and clean. The custom domain `lead-ai.us` DNS points to Vercel but remains linked to a legacy Vercel workspace project.
- **Action:** Re-assign domain `lead-ai.us` to project `lead-ai-us` in Vercel Dashboard.

---

## TIER 2 — CONTACT FLOW & LEAD CAPTURE

### G-002: Contact Form Server-Side Endpoint
- **Status:** MAILTO ONLY (TRUTHFUL)
- **Finding:** Contact form currently formats an email draft using `mailto:` without claiming server-side persistence.
- **Action for Phase 1:** Build `/api/contact` route and Firestore persistence collection.

### G-003: Chatbot Contact Persistence
- **Status:** LOCAL-ONLY (TRUTHFUL)
- **Finding:** Concierge chat widget saves state in `localStorage` and provides copy/mailto actions.
- **Action for Phase 1:** Connect chat widget to `/api/chat` or Firebase function backend.

---

## TIER 3 — MODULE IMPLEMENTATIONS

### G-004: Scaffold Repositories
- **Status:** SCAFFOLD ONLY
- **Finding:** Repositories `lead-ai-platform`, `lead-ai-whatsapp-agent`, `lead-ai-website-chatbot`, `lead-ai-lead-scoring-api`, `lead-ai-prompt-vault`, `lead-ai-firebase-saas-starter`, and `lead-ai-fraud-shield` are initial scaffolds.
- **Action for Phase 1:** Implement modular features starting with auth/Firestore baseline (`lead-ai-firebase-saas-starter`).

---

## TIER 4 — SECURITY & DEPENDENCIES

### G-005: Dependency Audit Remediation
- **Status:** DOCUMENTED FOR PHASE 1
- **Finding:** `npm audit` reports 17 vulnerabilities (14 high, 3 moderate). Build passes cleanly and no production-reachable security exploits detected in main Vite bundle.
- **Action for Phase 1:** Apply targeted, non-breaking package dependency updates.
