# Lead.AI Phase 1 — Conversion Architecture & Lead Funnel
**Last Verified:** 2026-08-08  

---

## 1. CUSTOMER JOURNEY LIFECYCLE

```text
Visitor Arrival (Hero: "Turn More Customer Conversations Into Organized Workflows")
   │
   ├── Path A: Start Free AI Audit (Low-friction entry -> lead-ai-business-audit.vercel.app)
   │
   └── Path B: Request Consultation (High-intent entry -> ConsultationModal intake form)
         │
         ├── Select Service Interest (Starter Setup, Growth System, Support, Custom)
         ├── Fill Contact & Business Challenge details
         └── Submit -> Logged to Lead Pipeline + Email/Notification Bridge
```

---

## 2. CONSULTATION DATA SCHEMA

```typescript
interface LeadAIContactRequest {
  id: string;
  source: "website_consultation_modal" | "free_audit" | "chatbot" | "contact_page";
  name: string;
  email: string;
  phone?: string;
  businessName?: string;
  businessType: string;
  serviceRequested: string;
  message?: string;
  consent: boolean;
  status: "new" | "reviewed" | "contacted" | "closed";
  createdAt: string;
}
```
