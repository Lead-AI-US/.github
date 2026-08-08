# Lead.AI Phase 2 — Data Model & Collection Specification
**Last Verified:** 2026-08-08  

---

## 1. CANONICAL `leads` COLLECTION

```typescript
export type LeadSource =
  | "website"
  | "business_audit"
  | "website_chatbot"
  | "whatsapp"
  | "manual"
  | "other";

export type LeadStatus =
  | "new"
  | "reviewed"
  | "contacted"
  | "consultation_requested"
  | "qualified"
  | "implementation_discussion"
  | "not_ready"
  | "closed";

export interface LeadRecord {
  id: string; // crypto.randomUUID()
  source: LeadSource;
  name: string;
  email: string;
  phone?: string | null;
  businessName?: string | null;
  businessType?: string | null;
  requestedService?: string | null;
  message?: string | null;
  status: LeadStatus;
  consent: boolean;
  sourceMetadata?: {
    path?: string;
    campaign?: string;
    referrer?: string;
    userAgent?: string;
  };
  createdAt: string; // ISO 8601 Timestamp
  updatedAt: string;
  schemaVersion: number; // 1
}
```

---

## 2. APPEND-ONLY `lead_activities` COLLECTION

```typescript
export type ActivityType =
  | "lead_created"
  | "status_changed"
  | "note_added"
  | "email_notification_sent"
  | "email_notification_failed"
  | "customer_acknowledgement_sent"
  | "follow_up_recorded";

export interface LeadActivity {
  id: string;
  leadId: string;
  type: ActivityType;
  actorType: "system" | "user";
  actorId?: string | null;
  metadata?: Record<string, any>;
  createdAt: string;
}
```
