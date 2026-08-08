# Lead.AI Phase 7 — Pilot Launch & Observability Architecture
**Last Verified:** 2026-08-08

---

## 1. OBSERVABILITY & ANALYTICS PIPELINE

```text
       Customer / User Action
                 │
                 ▼
     ProductAnalyticsService (trackProductEvent)
                 │
  Privacy-Filter (Strips emails, phone, tokens, credentials)
                 │
                 ▼
  workspaces/{workspaceId}/analyticsEvents
                 │
                 ▼
      /app/analytics Dashboard
```

---

## 2. AI QUALITY AUDITING & EMERGENCY SWITCHES

- **AI Quality Evaluator:** `src/lib/ai/aiQualityEvaluator.ts` audits response groundedness, helpfulness, zero-pricing compliance, and handoff accuracy.
- **Golden Regression Suite:** `src/test/aiGoldenSet.test.ts` (10 core test scenarios).
- **Emergency Kill Switches:** `src/lib/services/pilotService.ts` allows single-workspace emergency pausing (`websiteChat`, `whatsapp`, `booking`, `workflows`).
