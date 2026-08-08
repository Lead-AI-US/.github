# Lead.AI Phase 5 — Multi-Tenant Architecture Specification
**Last Verified:** 2026-08-08

---

## 1. MULTI-TENANT SYSTEM TOPOLOGY

```text
                    Lead.AI SaaS Platform
                              │
          ┌───────────────────┼───────────────────┐
          ▼                   ▼                   ▼
      Workspace A         Workspace B         Workspace C
  (ws_a1b2c3d4)       (ws_x9y8z7w6)       (ws_lead_ai_internal)
          │                   │                   │
  ┌───────┼───────┐   ┌───────┼───────┐   ┌───────┼───────┐
  ▼       ▼       ▼   ▼       ▼       ▼   ▼       ▼       ▼
Leads   Convs   Appts Leads   Convs   Appts Leads   Convs   Appts
  │       │       │   │       │       │   │       │       │
  └───────┼───────┘   └───────┼───────┘   └───────┼───────┘
          ▼                   ▼                   ▼
     Automations         Automations         Automations
     Knowledge           Knowledge           Knowledge
```

---

## 2. TENANT ISOLATION MODEL (Option A Hierarchy)

- **Root Collections (Platform-Level):**
  - `workspaces/{workspaceId}` — Workspace configuration, entitlements, widget key
  - `workspaceMembers/{memberId}` — User to workspace role mapping
  - `users/{userId}` — Registered Firebase Auth user profiles
  - `processedEvents/{eventId}` — Shared webhook idempotency registry

- **Subcollections (Tenant-Scoped Data):**
  - `workspaces/{workspaceId}/leads/{leadId}`
  - `workspaces/{workspaceId}/conversations/{conversationId}`
  - `workspaces/{workspaceId}/appointments/{appointmentId}`
  - `workspaces/{workspaceId}/bookingRequests/{requestId}`
  - `workspaces/{workspaceId}/workflowRuns/{runId}`
  - `workspaces/{workspaceId}/scheduledActions/{actionId}`
  - `workspaces/{workspaceId}/followUps/{followUpId}`
  - `workspaces/{workspaceId}/knowledgeSources/{sourceId}`

---

## 3. SECURITY & AUTHORIZATION GATEWAY

All `/api/admin/*` and privileged workspace endpoints are guarded by `requireAuthContext()` middleware (`src/lib/auth/serverAuth.ts`):
1. Verifies Firebase Auth ID Token (`Authorization: Bearer <idToken>`).
2. Derives verified `userId` and `email` from token (never trusts request body).
3. Queries `workspaceMembers` to verify user membership and role (`owner`, `admin`, `member`, `viewer`).
4. Rejects unauthenticated calls with `401 Unauthorized` and unauthorized workspace calls with `403 Forbidden`.
