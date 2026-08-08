# Lead.AI Phase 4 — Workflow Engine Specification
**Last Verified:** 2026-08-08

---

## 1. CURATED WORKFLOW TEMPLATES

| ID | Name | Trigger | Steps |
|----|------|---------|-------|
| `wf-consultation-booking` | Consultation Booking | `consultation_requested` | 5 |
| `wf-appointment-reminder` | Appointment Reminder | `appointment_created` | 4 |
| `wf-post-consultation-task` | Post-Consultation Follow-Up Task | `appointment_completed` | 2 |
| `wf-appointment-cancelled` | Appointment Cancellation Handler | `appointment_cancelled` | 3 |

---

## 2. DURABLE SCHEDULER

- **Infrastructure:** Vercel Cron (`*/5 * * * *`) + Firestore `scheduledActions` collection.
- **Scheduler Endpoint:** `POST /api/scheduler/tick` secured with `CRON_SECRET` Bearer token.
- **Execution Pattern:** Query due actions → claim atomically → execute → record result.
- **Idempotency:** Each action is claimed by updating `status: "processing"` before execution, preventing duplicate runs from parallel invocations.
- **Retry Policy:** Max 3 attempts with error tracking. Actions exceeding max attempts are marked `"failed"` and surfaced in the Automation Failure Inbox.

---

## 3. WORKFLOW STEP TYPES

- `add_activity` — Log operational event to audit trail.
- `update_lead_status` — Update canonical lead status.
- `wait` — Create a `ScheduledAction` for future resumption; pause run as `"waiting"`.
- `request_human_approval` — Pause run as `"waiting_for_approval"` until operator action.
- `schedule_reminder` — Delegate to `reminderService.scheduleReminder()` with offset from appointment.
- `cancel_reminders` — Delegate to `reminderService.cancelAppointmentReminders()`.
- `check_suppression` — Verify communication suppression before proceeding.
- `condition` — Evaluate context field for conditional branching.
