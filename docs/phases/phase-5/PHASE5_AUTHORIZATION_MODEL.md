# Lead.AI Phase 5 — Authorization & Role-Based Access Control
**Last Verified:** 2026-08-08

---

## 1. ROLE PERMISSION MATRIX

| Feature | Owner | Admin | Member | Viewer |
|---------|-------|-------|--------|--------|
| Workspace Settings | ✅ | ✅ | ❌ | ❌ |
| Manage Members / Invite | ✅ | ✅ | ❌ | ❌ |
| Manage Integrations / Keys | ✅ | ✅ | ❌ | ❌ |
| View Leads & Inbox | ✅ | ✅ | ✅ | ✅ |
| Update Lead & Handoff | ✅ | ✅ | ✅ | ❌ |
| Approve Follow-Up Drafts | ✅ | ✅ | ❌ | ❌ |
| Configure Knowledge Base | ✅ | ✅ | ❌ | ❌ |
| View Automations | ✅ | ✅ | ✅ | ✅ |

---

## 2. SERVER-SIDE ROLE DERIVATION

Client-submitted `operatorId`, `role`, or `workspaceId` values are never trusted. The server verifies the token signature via `adminApp.auth().verifyIdToken()`, extracts the `uid`, looks up membership in Firestore `workspaceMembers`, and derives the true `role` and `workspaceId` server-side.
