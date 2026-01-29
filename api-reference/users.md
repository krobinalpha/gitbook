# Users

Public endpoint for user profile by wallet address. No authentication required.

---

## GET /api/users/:address

Get public user profile by wallet address.

**Path parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `address` | string | Wallet address (0x + 40 hex chars). Must match a registered user's primary or linked wallet. |

**Response:** User object (e.g. `id`, `username`, `email`, `bio`, `avatar`, `address`, `walletAddresses`, `website`, `twitter`, `telegram`, `discord`, `github`, `tokensCreated`, `totalVolume`, `totalVolumeUSD`, `isVerified`). Returns 404 if user not found.
