# Lead.AI Phase 4 — Booking & Appointment Domain Model
**Last Verified:** 2026-08-08

---

## 1. `bookingRequests` COLLECTION

```typescript
interface BookingRequest {
  id: string;
  leadId?: string | null;
  conversationId?: string | null;
  source: "website" | "website_chatbot" | "whatsapp" | "business_audit" | "admin";
  serviceType?: string | null;
  timezone: string;
  preferredDate?: string | null;
  notes?: string | null;
  status: "requested" | "confirmed" | "cancelled" | "expired" | "failed";
  appointmentId?: string | null;
  createdAt: string;
  updatedAt: string;
  schemaVersion: number; // 1
}
```

---

## 2. `appointments` COLLECTION

```typescript
interface Appointment {
  id: string;
  leadId?: string | null;
  conversationId?: string | null;
  bookingRequestId?: string | null;
  provider: string; // "stub" | "google_calendar"
  externalEventId?: string | null;
  title: string;
  startAt: string; // ISO 8601 UTC
  endAt: string;
  timezone: string;
  status: "tentative" | "confirmed" | "cancelled" | "completed" | "no_show";
  meetingLocation?: { type: "online" | "phone" | "in_person" | "other"; value?: string | null } | null;
  createdAt: string;
  updatedAt: string;
}
```

---

## 3. DOUBLE-BOOKING PROTECTION

Before finalizing an appointment, `confirmBooking()` checks for any existing non-cancelled appointment with an overlapping time range:

```typescript
const conflicts = appointments.filter(
  (a) => a.status !== "cancelled" && a.startAt < slotEndAt && a.endAt > slotStartAt
);
if (conflicts.length > 0) throw new Error("SLOT_CONFLICT");
```

Client receives `409 Conflict` with `code: "SLOT_CONFLICT"` and a user-facing message. No false confirmation is ever returned.
