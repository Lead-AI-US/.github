# Lead.AI Phase 2 — Serverless API Specification
**Last Verified:** 2026-08-08  

---

## 1. `POST /api/contact` ENDPOINT

- **Purpose:** Truthful lead consultation intake & datastore persistence.
- **Request Headers:** `Content-Type: application/json`
- **Request Payload:**
```json
{
  "name": "Jane Doe",
  "email": "jane@company.com",
  "phone": "+15550000000",
  "businessName": "Acme Services",
  "businessType": "local_services",
  "requestedService": "Growth Automation System",
  "message": "We need help automating lead follow-up...",
  "consent": true,
  "source": "website"
}
```

- **Success Response (200 OK):**
```json
{
  "success": true,
  "requestId": "550e8400-e29b-41d4-a716-446655440000",
  "status": "new",
  "message": "Lead consultation request recorded successfully."
}
```

- **Error Responses:**
  - `400 Bad Request`: Validation failure or missing consent.
  - `405 Method Not Allowed`: Invalid HTTP verb.
  - `500 Internal Server Error`: Server failure with generic client messaging.

---

## 2. `GET /api/health` ENDPOINT

- **Response (200 OK):**
```json
{
  "status": "ok",
  "service": "lead-ai-api",
  "version": "2.0.0",
  "timestamp": "2026-08-08T15:22:00.000Z"
}
```
