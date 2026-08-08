# Lead.AI Phase 3 — Omnichannel Architecture Specification
**Last Verified:** 2026-08-08  
**Phase 3 Status:** GREEN / VERIFIED  

---

## 1. OMNICHANNEL ENGINE TOPOLOGY

```text
               Website Visitor                      WhatsApp Customer
                      │                                    │
                      ▼                                    ▼
               Website Chatbot                   Twilio WhatsApp Webhook
             (/api/chat/message)                  (/api/whatsapp/webhook)
                      │                                    │
                      └─────────────────┬──────────────────┘
                                        ▼
                            Shared Conversation Engine
                           (src/lib/services/conversationService.ts)
                                        │
                      ┌─────────────────┼─────────────────┐
                      ▼                 ▼                 ▼
               Approved Knowledge   AI Safety Router  Human Handoff
                (knowledgeService)  (aiOrchestrator)    (Handoff)
                      │                 │                 │
                      └─────────────────┼─────────────────┘
                                        ▼
                              Canonical Lead System
                             (Phase 2 Firestore `leads`)
                                        │
                                        ▼
                              CRM Admin Workspace
                            (/admin/conversations)
```

---

## 2. ADAPTER RESPONSIBILITIES

- **Website Chatbot Adapter (`api/chat/`):** Manages anonymous chat session UUIDs, handles message submission, runs AI Orchestrator decision, stores messages, and supports human handoff requests.
- **WhatsApp Webhook Adapter (`api/whatsapp/webhook.ts`):** Verifies Twilio request signatures (`X-Twilio-Signature`), enforces `MessageSid` deduplication, normalizes inbound WhatsApp payloads, queries Conversation Engine, and outputs formatted TwiML XML responses.
- **AI Safety Orchestrator (`src/lib/ai/aiOrchestrator.ts`):** Classifies user intent, queries approved Lead.AI knowledge sources, enforces strict zero-pricing rules, and formats structured decisions (`AssistantDecision`).
- **CRM Omnichannel Inbox (`/admin/conversations`):** Single inbox for operators to inspect live Web & WhatsApp timelines, accept human handoffs, send operator messages, or return conversations to automated mode.
