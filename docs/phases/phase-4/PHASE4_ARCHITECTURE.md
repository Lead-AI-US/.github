# Lead.AI Phase 4 — Architecture Specification
**Last Verified:** 2026-08-08

---

## 1. PHASE 4 AUTOMATION LIFECYCLE TOPOLOGY

```text
Website Chat ───────────┐
                        │
WhatsApp ───────────────┤
                        │
Business Audit ─────────┤
                        ▼
                  Lead.AI CRM
                        │
                        ▼
                 Intent / Trigger
                        │
                        ▼
                  Workflow Engine
                 (workflowEngine.ts)
                        │
        ┌───────────────┼────────────────┐
        │               │                │
        ▼               ▼                ▼
     Booking         Follow-Up        Reminder
  (bookingService) (followUpService) (reminderService)
        │               │                │
        ▼               ▼                ▼
    Calendar          Email          Email/WhatsApp
        │               │                │
        └───────────────┼────────────────┘
                        ▼
                  Activity Timeline
                        │
                        ▼
                      CRM
```

---

## 2. COMPONENT RESPONSIBILITIES

- **`api/bookings/request.ts`:** Creates durable `BookingRequest` and triggers `consultation_requested` workflow.
- **`api/bookings/availability.ts`:** Returns real availability slots from the stub provider (Google Calendar adapter ready).
- **`api/bookings/confirm.ts`:** Re-verifies slot availability, commits `Appointment` atomically via Firestore batch, schedules 24h and 1h email reminders, triggers `appointment_created` workflow.
- **`api/scheduler/tick.ts`:** Secured Vercel Cron endpoint (every 5 minutes) querying and claiming due `scheduledActions`, processing them idempotently with bounded retries.
- **`workflowEngine.ts`:** 4 curated durable workflow templates backed by Firestore `workflowRuns` and `scheduledActions` collections.
- **`reminderService.ts`:** Schedules reminders with suppression checks; cancels all pending reminders when an appointment is cancelled.
- **`followUpService.ts`:** Creates follow-ups that always start as `approval_required` — human operator must explicitly approve before any outbound send.

---

## 3. PHASE 3 HARDENING INCLUDED

- **Durable Twilio deduplication:** Firestore `processedEvents/{MessageSid}` Firestore transaction (replaces in-memory `Set`).
- **Fail-closed Twilio validation:** Missing `TWILIO_AUTH_TOKEN` in production → `503 Service Unavailable`.
- **CORS hardening:** All chat API endpoints restricted to `lead-ai.us`, `lead-ai-us.vercel.app`, localhost.
- **Message length guard:** Chat messages capped at 2000 characters.
