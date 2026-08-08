# Lead.AI Phase 6 — Integration Secret Vault & Encryption Architecture
**Last Verified:** 2026-08-08

---

## 1. AES-256-GCM CREDENTIAL ENCRYPTION

To prevent customer credentials, OAuth tokens, and integration API keys from being stored in plain text or returned to browser clients:

- **Encryption Module:** `src/lib/security/secretVault.ts`
- **Algorithm:** `AES-256-GCM` with random 12-byte initialization vectors (IV) and authentication tags.
- **Master Key:** Derived via SHA-256 hash of `SERVER_SECRET_KEY` / `CRON_SECRET`.
- **Storage Location:** `workspaces/{workspaceId}/secrets/{secretKeyName}`.

---

## 2. API SECRET RETRIEVAL POLICY

1. React browser client never receives decrypted credentials.
2. Serverless API handlers (`api/*`) decrypt credentials server-side inside Node.js execution environment using `decryptSecret()`.
3. Secret updates require `owner` or `admin` workspace role.
