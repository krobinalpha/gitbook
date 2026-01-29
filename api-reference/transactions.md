# Transactions

Public endpoints for on-chain transaction data. No authentication required.

---

## GET /api/transactions/token/:tokenAddress

Get transactions for a token (buys, sells, etc.).

**Path parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `tokenAddress` | string | Token contract address (0x + 40 hex chars) |

**Query parameters (all optional):**

| Parameter | Type | Description |
|-----------|------|-------------|
| `page` | integer (min 1) | Page number (default: 1) |
| `pageSize` | integer (1–100) | Items per page (default: 10) |
| `chainId` | integer (min 1) | Chain ID |

**Response:** Paginated list of transactions (e.g. `data`, `transactions`, `totalCount`, `currentPage`, `totalPages`, `hasNextPage`, `hasPrevPage`). Sorted by block timestamp descending.

---

## GET /api/transactions/address/:address

Get transactions for a wallet address (as sender or recipient).

**Path parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `address` | string | Wallet address (0x + 40 hex chars) |

**Query parameters (all optional):**

| Parameter | Type | Description |
|-----------|------|-------------|
| `page` | integer (min 1) | Page number |
| `pageSize` | integer (1–100) | Items per page |
| `chainId` | integer (min 1) | Filter by chain ID |

**Response:** Paginated list of transactions involving the address.
