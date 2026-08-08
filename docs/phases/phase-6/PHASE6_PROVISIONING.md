# Lead.AI Phase 6 — Customer Provisioning & Activation Engine
**Last Verified:** 2026-08-08

---

## 1. PROVISIONING LIFECYCLE

```text
Customer Signup → 6-Step Onboarding → Provision Workspace → Validate Checklist → Activate Workspace
```

1. **Idempotent Workspace Creation:** `createWorkspace()` creates `workspaces/{workspaceId}` document and owner `workspaceMembers` record.
2. **Default Initialization:** Initializes baseline knowledge sources, default workflow definitions (`wf-consultation-booking`, `wf-appointment-reminder`), and public widget embed keys (`publicWidgetKey`).
3. **Activation Validation:** `validateWorkspaceActivation()` verifies business profile completeness, approved knowledge presence, and channel readiness.
4. **Server Activation:** `POST /api/workspaces/activate` updates status to `"active"` only when blocking checklist items pass.
