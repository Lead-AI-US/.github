# Lead.AI Phase 4.1 — Security & Concurrency Verification
**Last Verified:** 2026-08-08

---

## 1. SCHEDULER FAIL-CLOSED AUTHENTICATION VERIFICATION

`/api/scheduler/tick` has been hardened to fail closed:

```typescript
const cronSecret = process.env.CRON_SECRET;
const authHeader = req.headers.authorization;

if (!cronSecret) {
  return res.status(503).json({ error: "Scheduler configuration error. CRON_SECRET is missing." });
}

if (authHeader !== `Bearer ${cronSecret}`) {
  return res.status(401).json({ error: "Unauthorized" });
}
```

### Verified Behaviors:
- **`CRON_SECRET` missing:** Returns `503 Service Unavailable`
- **Missing Authorization header:** Returns `401 Unauthorized`
- **Wrong Bearer token:** Returns `401 Unauthorized`
- **Valid Bearer token:** Returns `200 OK` with execution report

---

## 2. CONCURRENCY & IDEMPOTENCY GUARD

To prevent parallel cron workers or API retries from double-processing actions or creating duplicate calendar events:

1. **Atomic Action Claiming:**
   Each `ScheduledAction` is claimed using a Firestore transaction (`runTransaction`):
   ```typescript
   claimed = await adminDb.runTransaction(async (tx) => {
     const freshDoc = await tx.get(actionRef);
     if (freshDoc.data().status !== "scheduled") return false;
     tx.update(actionRef, { status: "processing", attempts: currentAttempts + 1 });
     return true;
   });
   ```

2. **Idempotent Appointment Confirmation:**
   `confirmBooking()` checks if `bookingRequest.status === "confirmed"`. If an appointment already exists, it returns the existing appointment without creating duplicate Google Calendar events.

3. **Orphan Rollback:**
   If external calendar creation succeeds but Firestore batch commit fails, `confirmBooking()` calls `provider.cancelEvent(externalEventId)` to delete the orphan calendar event.

---

## 3. FIRESTORE AUTHORITATIVE SOURCE OF TRUTH

Browser `localStorage` has been removed from all authoritative server-side paths (`api/bookings/*`, `api/scheduler/*`, `api/admin/*`). Client local storage is used solely for offline fallback in administrative UI views.
