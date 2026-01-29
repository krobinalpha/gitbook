# 📈 Histories

Public endpoints for token price history. No authentication required.

**For trading bots:** Use for charts or backfilling price series. Response is an array of points; each point includes `timestamp` and `price` (or equivalent chart fields). Sorted ascending by time (oldest first).

***

## GET /api/histories/token/:tokenAddress

Get price history for a token (for charts).

**Path parameters:**

| Parameter      | Type   | Description                                |
| -------------- | ------ | ------------------------------------------ |
| `tokenAddress` | string | Token contract address (0x + 40 hex chars) |

**Query parameters (all optional):**

| Parameter | Type             | Description                                                |
| --------- | ---------------- | ---------------------------------------------------------- |
| `chainId` | integer (min 1)  | Chain ID (optional; can be inferred from token if omitted) |
| `limit`   | integer (1–1000) | Max number of history points (default: 100)                |

**Response:** Array of history entries. Each entry: `timestamp` (ISO or numeric), `price` (or fields used for chart series). Sorted ascending by timestamp (oldest to newest).
