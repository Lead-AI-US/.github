# Lead.AI Phase 6 — Customer Provisioning & Operations Architecture
**Last Verified:** 2026-08-08

---

## 1. APPLICATION LAYER ARCHITECTURE

```text
               Authenticated Customer / User
                             │
                             ▼
             WorkspaceProvider (WorkspaceContext)
                             │
             ProtectedRoute & Auth State Guard
                             │
            Consolidated SaaS Route Hierarchy
   (/app, /app/leads, /app/conversations, /app/appointments...)
                             │
    ┌────────────────────────┼────────────────────────┐
    ▼                        ▼                        ▼
Workspace API           Secret Vault            Health Center
(/api/workspaces)     (AES-256-GCM Crypto)    (/app/health Audit)
```

---

## 2. CLIENT STATE & WORKSPACE ISOLATION

- **Zero Hardcoded Workspaces:** Hardcoded fallbacks to `ws_lead_ai_internal` inside client components have been completely removed.
- **WorkspaceContext:** `useWorkspaceContext()` queries `GET /api/workspaces` via Firebase Auth Bearer ID token.
- **Automatic Routing:**
  - 0 workspaces → `/onboarding`
  - 1 workspace → active workspace set
  - >1 workspaces → saved `lastWorkspaceId` restored if authorized
- **Cache Scoping:** TanStack Query keys are namespaced by `workspaceId` and cleared on workspace context switch.
