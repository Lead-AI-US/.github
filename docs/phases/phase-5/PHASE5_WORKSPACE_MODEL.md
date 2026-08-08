# Lead.AI Phase 5 — Workspace & Membership Domain Specification
**Last Verified:** 2026-08-08

---

## 1. WORKSPACE DOMAIN SCHEMAS

```typescript
interface Workspace {
  id: string; // e.g. ws_1770567000_abc123
  name: string;
  slug: string;
  status: "onboarding" | "active" | "suspended" | "archived";
  businessType?: string | null;
  timezone: string;
  ownerUserId: string;
  publicWidgetKey: string; // Embed identifier for website widget
  allowedOrigins?: string[];
  entitlements: WorkspaceEntitlements;
  createdAt: string;
  updatedAt: string;
  schemaVersion: number; // 1
}

interface WorkspaceMember {
  id: string;
  workspaceId: string;
  userId: string;
  userEmail: string;
  role: "owner" | "admin" | "member" | "viewer";
  status: "active" | "invited" | "disabled";
  createdAt: string;
  updatedAt: string;
}
```

---

## 2. BASELINE WORKSPACE (`ws_lead_ai_internal`)

All pre-existing Lead.AI operational records (Phase 0 - 4.1) are mapped to `ws_lead_ai_internal` to preserve 100% functionality of existing Lead.AI operations without data fragmentation.
