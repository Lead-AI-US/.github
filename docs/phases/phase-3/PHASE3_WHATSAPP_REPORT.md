# Lead.AI Phase 3 — WhatsApp Webhook Specification
**Last Verified:** 2026-08-08  

---

## 1. TWILIO WHATSAPP WEBHOOK (`POST /api/whatsapp/webhook`)

- **Signature Verification:** Enforces `twilio.validateRequest(authToken, signature, url, body)` when `TWILIO_AUTH_TOKEN` is present in environment.
- **Message Deduplication:** Stores processed `MessageSid` identifiers to prevent duplicate processing on webhook retries.
- **Normalized Inbound Flow:** Normalizes `From` phone and `Body` text into shared Conversation Engine (`getOrCreateConversation("whatsapp", phone)`).
- **Outbound Delivery:** Responds with valid Twilio TwiML XML payload (`<Response><Message>...</Message></Response>`).
