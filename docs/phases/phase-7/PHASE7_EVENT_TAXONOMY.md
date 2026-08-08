# Lead.AI Phase 7 — Product Event Taxonomy Specification
**Last Verified:** 2026-08-08

---

## 1. PRIVACY-FIRST EVENT SCHEMA

```typescript
interface ProductEvent {
  id: string;
  workspaceId: string;
  actorType: "visitor" | "customer" | "workspace_user" | "system";
  actorId?: string;
  eventName: EventName;
  source?: string;
  properties?: Record<string, string | number | boolean | null>;
  sessionId?: string;
  isTest?: boolean;
  occurredAt: string;
  schemaVersion: number; // 1
}
```

---

## 2. PRIVACY FILTER GUARANTEES

The `filterProperties()` helper in `analyticsService.ts` automatically strips the following keys before persisting events:
`email`, `phone`, `password`, `token`, `secret`, `auth`, `key`, `credential`.

---

## 3. CANONICAL EVENT TAXONOMY

- `signup_started`, `signup_completed`
- `workspace_created`, `onboarding_started`, `onboarding_completed`
- `workspace_activation_attempted`, `workspace_activated`
- `integration_connected`, `integration_failed`
- `conversation_started`, `message_received`, `assistant_response_generated`
- `handoff_requested`, `handoff_accepted`
- `lead_created`, `lead_qualified`, `lead_status_changed`
- `booking_requested`, `appointment_confirmed`, `appointment_cancelled`
- `workflow_started`, `workflow_completed`, `workflow_failed`
