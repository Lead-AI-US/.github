# Lead.AI Phase 6 — Self-Service Integration Directory
**Last Verified:** 2026-08-08

---

## 1. INTEGRATION CATEGORIES

| Channel | Implementation | Health Check Verification |
|---------|----------------|--------------------------|
| **Website Chat Widget** | Public embed script with `data-widget-key` | Allowed origins CORS guard & 2000-char length check |
| **Google Calendar** | Google FreeBusy API + OAuth / Service Account | Calendar FreeBusy query & double-booking transaction check |
| **WhatsApp Automation** | Twilio WhatsApp Webhook | Fail-closed Twilio signature validation & durable dedup |
| **Transactional Email** | Resend API Integration | Operational metadata logging & internal lead alerts |

---

## 2. EMBEDDABLE WIDGET SNIPPET

```html
<script
  src="https://lead-ai.us/widget.js"
  data-widget-key="PUBLIC_WIDGET_KEY"
  async>
</script>
```

Public widget keys identify workspace chat configuration without authorizing administrative operations.
