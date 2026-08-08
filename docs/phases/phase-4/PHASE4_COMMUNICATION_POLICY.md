# Lead.AI Phase 4 — Communication Policy
**Last Verified:** 2026-08-08

---

## 1. ZERO PUBLIC PRICING POLICY

All automated messages — chatbot replies, WhatsApp responses, booking confirmations, reminder emails, and follow-up drafts — must **never** contain:
- Dollar amounts ($)
- Setup fees or monthly fees
- Package prices or tiers
- Revenue projections or ROI claims

---

## 2. HUMAN APPROVAL REQUIRED FOR SALES FOLLOW-UP

All outbound sales follow-up messages begin in `status: "approval_required"`. The operator must:
1. Review the AI-generated draft in `/admin/approvals`.
2. Edit if necessary to ensure compliance with communication policy.
3. Explicitly approve to queue for delivery.

**Transactional messages** (booking confirmations, reminders) may be sent without approval per `AutomationPolicy.automaticTransactionalRemindersEnabled`.

---

## 3. SUPPRESSION SYSTEM

Before any outbound action, the system checks `CommunicationSuppression` records:
- `opt_out` — Customer explicitly opted out.
- `invalid_contact` — Contact information known to be invalid.
- `operator` — Manually suppressed by an operator.
- `policy` — Suppressed due to channel policy violation.

Suppressed contacts never receive automated messages.

---

## 4. STOP CONDITIONS

Automation stops when:
- Customer opts out.
- Appointment is confirmed and workflow goal is achieved.
- Lead is `closed`.
- Operator cancels workflow run.
- Hard delivery failure (max retries exceeded).
