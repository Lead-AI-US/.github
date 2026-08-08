# Lead.AI Phase 3 — Conversation Domain Model
**Last Verified:** 2026-08-08  

---

## 1. CANONICAL `conversations` SCHEMA

```typescript
export type ConversationChannel = "website" | "whatsapp";

export type ConversationStatus =
  | "active"
  | "waiting_for_customer"
  | "waiting_for_human"
  | "human_active"
  | "resolved"
  | "closed";

export type ConversationMode = "automation" | "human" | "hybrid";

export interface Conversation {
  id: string; // UUID
  channel: ConversationChannel;
  externalConversationId?: string | null;
  leadId?: string | null;
  status: ConversationStatus;
  currentMode: ConversationMode;
  startedAt: string; // ISO 8601 Timestamp
  lastMessageAt: string;
  updatedAt: string;
  schemaVersion: number; // 1
}
```

---

## 2. CANONICAL `messages` SCHEMA

```typescript
export type MessageRole = "customer" | "assistant" | "human" | "system";

export interface ConversationMessage {
  id: string;
  conversationId: string;
  channel: ConversationChannel;
  role: MessageRole;
  content: string;
  externalMessageId?: string | null;
  deliveryStatus?: "received" | "queued" | "sent" | "delivered" | "failed";
  createdAt: string;
}
```
