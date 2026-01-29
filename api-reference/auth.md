# Auth

Public auth **entry points** used to obtain a session. No Bearer token required to call these. Endpoints that require an existing session (e.g. `/auth/me`, `/auth/smart-wallet`) or admin-only flows are not documented here.

---

## POST /api/auth/nonce

Generate a nonce for Sign-In with Ethereum (SIWE). The client signs a SIWE message containing this nonce and then calls `POST /api/auth/verify-wallet`.

**Request body:**

| Field | Type | Description |
|-------|------|-------------|
| `address` | string (required) | Wallet address (0x + 40 hex chars) |

**Response:** `{ "nonce": "<hex string>" }`. Nonce expires after a short time (e.g. 10 minutes).

---

## POST /api/auth/verify-wallet

Verify a SIWE signature and issue a JWT. Call after the user signs the SIWE message (built with the nonce from `POST /api/auth/nonce`).

**Request body:**

| Field | Type | Description |
|-------|------|-------------|
| `message` | string (required) | Full SIWE message string |
| `signature` | string (required) | EIP-191 signature (0x + 130 hex chars, 132 total) |
| `address` | string (required) | Wallet address that signed the message |

**Response:** `token` (JWT), `user` (id, address, username, email, avatar). Use the `token` in the `Authorization: Bearer <token>` header for authenticated endpoints (not documented in this reference).

---

## POST /api/auth/send-email-code

Send a one-time verification code to an email address. Used for email login or account linking.

**Request body:**

| Field | Type | Description |
|-------|------|-------------|
| `email` | string (required) | Valid email address |

**Response:** `{ "message": "Verification code sent to your email" }`. Code is valid for a short period (e.g. 10 minutes). Rate limits may apply.

---

## POST /api/auth/verify-email-code

Verify the email code and log in. Call after the user receives the code from `POST /api/auth/send-email-code`.

**Request body:**

| Field | Type | Description |
|-------|------|-------------|
| `email` | string (required) | Same email used in send-email-code |
| `code` | string (required) | 6-digit code (digits only) |

**Response:** `token` (JWT), `user` (id, address, username, email, avatar). Use the `token` for authenticated requests.

---

## POST /api/auth/social/:provider

Initiate social login (OAuth). Returns a URL to redirect the user to the provider. After the user completes the flow, the provider redirects to the backend callback; the frontend then receives the session (callback URLs are not documented as public API).

**Path parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `provider` | string | One of: `google`, `apple` |

**Request body (optional):**

| Field | Type | Description |
|-------|------|-------------|
| `redirectUri` | string | Frontend URL to return to after OAuth (optional; server may use default) |

**Response:** `{ "redirectUrl": "<OAuth URL>" }`. Redirect the user to `redirectUrl` to start the OAuth flow.
