# Lead.AI Phase 4 — Calendar Integration Specification
**Last Verified:** 2026-08-08

---

## 1. CURRENT STATUS: STUB AVAILABILITY PROVIDER

Phase 4 implements the full booking domain with a **stub availability service** that generates real availability slots based on configurable business hours:

- **Business Hours:** Monday–Friday, 9:00 AM – 5:00 PM ET (Friday until 3:00 PM)
- **Slot Duration:** 30 minutes
- **Buffer Between Slots:** 15 minutes
- **Minimum Notice:** 60 minutes
- **Max Booking Horizon:** 30 days

The stub service is **drop-in replaceable** with a Google Calendar adapter. The `getAvailability()` interface contract in `bookingService.ts` is designed to be swapped without changing any upstream API endpoints.

---

## 2. GOOGLE CALENDAR INTEGRATION PLAN (When Credentials Are Ready)

Replace `getAvailability()` with:

1. **Google Calendar API** (`GET /calendars/{calendarId}/freeBusy`) to check real busy periods.
2. **OAuth 2.0 Service Account** credentials stored as `GOOGLE_SERVICE_ACCOUNT_KEY` Vercel environment variable.
3. **Event creation** via `POST /calendars/{calendarId}/events` upon `confirmBooking()`.
4. Existing `Appointment.externalEventId` field stores the created Google Calendar event ID.

> [!IMPORTANT]
> Never expose Google OAuth tokens or service account JSON in client-side code, logs, or version control.
