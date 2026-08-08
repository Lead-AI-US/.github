# Lead.AI Phase 3 — Website Chatbot Specification
**Last Verified:** 2026-08-08  

---

## 1. BACKEND CHAT ENDPOINTS

- `POST /api/chat/session`: Creates or retrieves an anonymous website chat session using a client UUID.
- `POST /api/chat/message`: Handles user message submission, persists inbound message, runs AI Orchestrator decision, stores assistant reply, and returns decision context.
- `POST /api/chat/handoff`: Explicit user request for human operator intervention (`status: waiting_for_human`).

---

## 2. CHAT WIDGET FEATURES

- **Persistent Reload Support:** Anonymous session token stored in `localStorage` (`lead_ai_chat_session_id_v2`).
- **Real-Time UI:** Message timeline auto-scrolling, typing state indicators, quick audit links, and human team handoff trigger button.
- **Theme Integration:** Full light/dark/system theme support matching site tokens.
