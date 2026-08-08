# Lead.AI Phase 2 — Architecture Specification
**Last Verified:** 2026-08-08  
**Phase 2 Status:** GREEN / VERIFIED  

---

## 1. END-TO-END OPERATING SYSTEM TOPOLOGY

```text
               lead-ai.us Front-End
                        │
         ┌──────────────┴──────────────┐
         ▼                             ▼
  Free Business Audit         Consultation Modal
         │                             │
         └──────────────┬──────────────┘
                        │
                        ▼
               POST /api/contact
                        │
      ┌─────────────────┼─────────────────┐
      ▼                 ▼                 ▼
Zod Validation     Same-Origin CORS    Abuse Controls
      │                 │                 │
      └─────────────────┼─────────────────┘
                        │
                        ▼
              Firestore (`leads`)
                        │
         ┌──────────────┼──────────────┐
         ▼              ▼              ▼
   Resend Email   CRM Workspace   Activity Log
   Notification  (/admin/leads)  (`lead_activities`)
```

---

## 2. COMPONENT RESPONSIBILITIES

- **`/api/contact` Serverless API Handler:** Validates input payloads using Zod, creates document UUIDs, persists lead records directly into Firestore `leads` collection, appends `lead_activities`, and dispatches email notifications.
- **`ConsultationModal` Component:** Refactored for Truthful Interaction Standard. Requires confirmed 200 OK server persistence before showing receipt UI. Displays clear error state with form preservation and mailto fallback when offline.
- **CRM-lite Workspace (`/admin/leads`):** Protected administrative interface with Auth Gate, status filtering, lead detail drawers, internal notes, and audit activity timelines.
