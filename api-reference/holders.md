# 👥 Holders

Public endpoints for token holder data. No authentication required.

***

## GET /api/holders/token/:tokenAddress

Get holders of a token, sorted by share (percentage).

**Path parameters:**

| Parameter      | Type   | Description                                |
| -------------- | ------ | ------------------------------------------ |
| `tokenAddress` | string | Token contract address (0x + 40 hex chars) |

**Query parameters (all optional):**

| Parameter  | Type            | Description                                                |
| ---------- | --------------- | ---------------------------------------------------------- |
| `page`     | integer (min 1) | Page number (default: 1)                                   |
| `pageSize` | integer (1–100) | Items per page (default: 50)                               |
| `chainId`  | integer (min 1) | Chain ID (optional; can be inferred from token if omitted) |

**Response:** Paginated list of holders (e.g. `data` / `result` with `holderAddress`, `balance`, `balanceUSD`, `percentage`; `totalCount`, `currentPage`, `totalPages`, `hasNextPage`, `hasPrevPage`).

***

## GET /api/holders/address/:holderAddress

Get tokens held by a specific wallet address (only non-zero balances).

**Path parameters:**

| Parameter       | Type   | Description                               |
| --------------- | ------ | ----------------------------------------- |
| `holderAddress` | string | Holder wallet address (0x + 40 hex chars) |

**Query parameters (all optional):**

| Parameter  | Type            | Description        |
| ---------- | --------------- | ------------------ |
| `page`     | integer (min 1) | Page number        |
| `pageSize` | integer (1–100) | Items per page     |
| `chainId`  | integer (min 1) | Filter by chain ID |

**Response:** Paginated list of token holdings (e.g. `data` with token address, symbol, name, balance, balanceUSD, percentage, chainId, logo; pagination fields).

***

## GET /api/holders/address/:holderAddress/batch

Get all tokens held by an address in one call, with full token details (no pagination).

**Path parameters:**

| Parameter       | Type   | Description                               |
| --------------- | ------ | ----------------------------------------- |
| `holderAddress` | string | Holder wallet address (0x + 40 hex chars) |

**Query parameters (optional):**

| Parameter | Type            | Description        |
| --------- | --------------- | ------------------ |
| `chainId` | integer (min 1) | Filter by chain ID |

**Response:** List of holdings with token details (e.g. address, symbol, name, balance, balanceUSD, percentage, chainId, logo).
