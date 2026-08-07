# Lead.AI Next Actions
**Phase 0.5 → Phase 1 Transition Roadmap**  
**Last Verified:** 2026-08-07  

---

## IMMEDIATE ACTIONS FOR PHASE 1

### 1. Domain Alias Assignment (Control Plane)
- Assign `lead-ai.us` and `www.lead-ai.us` custom domains to Vercel project `lead-ai-us` (`aruns-projects-0839d12f`).

### 2. Server-Side Contact Endpoint (`lead-ai-firebase-saas-starter`)
- Implement server-side contact API endpoint `/api/contact`.
- Persist contact submissions to Firestore `contactRequests` collection.
- Send automated notification to system operator.

### 3. Shared Data Models & Firestore Security Rules
- Define standard TypeScript interfaces for `Lead`, `AuditReport`, `ContactRequest`, and `ChatSession`.
- Implement baseline Firestore rules ensuring zero public write/read leakage.

### 4. Dependency Security Upgrades
- Perform targeted `npm update` on non-breaking packages reported in `npm audit`.
- Re-run `npm run build` and typecheck to verify stability.

---

## MULTI-PHASE MODULE ROADMAP

```text
Phase 1: Backend Baseline (Contact API, Shared Schemas, Security Rules)
Phase 2: Product Microservices (Lead Scoring API, Chatbot Widget API)
Phase 3: Omnichannel Communication (WhatsApp Webhook & Twilio Integration)
Phase 4: SaaS Management Platform (Lead.AI Control Center Dashboard)
```
