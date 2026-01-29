# 💸 Transactions

Public endpoints for on-chain transaction data. No authentication required.

**For trading bots:** Poll `GET /api/transactions/token/:tokenAddress` for recent buys/sells; combine with WebSocket for real-time trades plus history. Each item includes `type` (Bought/Sold), `txHash`, `blockTimestamp`, `ethAmount`, `tokenAmount`, `senderAddress`, `recipientAddress`; amounts are wei strings unless the API documents otherwise.

***

## GET /api/transactions/token/:tokenAddress

Get transactions for a token (buys, sells, etc.).

**Path parameters:**

| Parameter      | Type   | Description                                |
| -------------- | ------ | ------------------------------------------ |
| `tokenAddress` | string | Token contract address (0x + 40 hex chars) |

**Query parameters (all optional):**

| Parameter  | Type            | Description                  |
| ---------- | --------------- | ---------------------------- |
| `page`     | integer (min 1) | Page number (default: 1)     |
| `pageSize` | integer (1–100) | Items per page (default: 10) |
| `chainId`  | integer (min 1) | Chain ID                     |

**Response:** Paginated list. Top-level: `data` (or `transactions`), `totalCount`, `currentPage`, `totalPages`, `hasNextPage`, `hasPrevPage`. Each transaction: `type` (Bought/Sold), `txHash`, `blockNumber`, `blockTimestamp`, `ethAmount`, `tokenAmount`, `senderAddress`, `recipientAddress`, `chainId`. Sorted by block timestamp descending.

***

## GET /api/transactions/address/:address

Get transactions for a wallet address (as sender or recipient).

**Path parameters:**

| Parameter | Type   | Description                        |
| --------- | ------ | ---------------------------------- |
| `address` | string | Wallet address (0x + 40 hex chars) |

**Query parameters (all optional):**

| Parameter  | Type            | Description        |
| ---------- | --------------- | ------------------ |
| `page`     | integer (min 1) | Page number        |
| `pageSize` | integer (1–100) | Items per page     |
| `chainId`  | integer (min 1) | Filter by chain ID |

**Response:** Paginated list of transactions involving the address.
