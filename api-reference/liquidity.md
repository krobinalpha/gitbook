# Liquidity

Public endpoints for liquidity events. No authentication required.

---

## GET /api/liquidity-events

Get liquidity events for a token (e.g. graduation, LP adds).

**Query parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `tokenAddress` | string (required) | Token contract address (0x + 40 hex chars) |
| `page` | integer (min 1) | Page number (optional, default: 1) |
| `pageSize` | integer (1–100) | Items per page (optional, default: 20) |
| `chainId` | integer (min 1) | Chain ID (optional; can be inferred from token if omitted) |

**Response:** Paginated list of liquidity events (e.g. event type, block timestamp, token info). Sorted by block timestamp descending.
