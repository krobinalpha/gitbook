# Tokens

Public endpoints for token listing and token details. No authentication required.

***

## GET /api/tokens

Get all tokens with pagination and optional filters.

**Query parameters (all optional):**

| Parameter                      | Type              | Description                                                                                                            |
| ------------------------------ | ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `page`                         | integer (min 1)   | Page number (default: 1)                                                                                               |
| `pageSize`                     | integer (1–100)   | Items per page (default: 20)                                                                                           |
| `sortBy`                       | string            | One of: `createdAt`, `currentPriceUSD`, `marketCapUSD`, `volume24hUSD`, `priceChange24hPercent` (default: `createdAt`) |
| `sortOrder`                    | string            | `asc` or `desc` (default: `desc`)                                                                                      |
| `chainId`                      | integer (min 1)   | Filter by chain ID                                                                                                     |
| `verified`                     | boolean           | Filter by verified status                                                                                              |
| `active`                       | boolean           | Filter by active status                                                                                                |
| `minPrice`, `maxPrice`         | number (≥ 0)      | Price range filter                                                                                                     |
| `minMarketCap`, `maxMarketCap` | number (≥ 0)      | Market cap range filter                                                                                                |
| `timeRange`                    | string            | One of: `1h`, `24h`, `7d`, `30d`, `all`                                                                                |
| `startDate`, `endDate`         | string (ISO 8601) | Date range filter                                                                                                      |

**Response:** Paginated list of tokens (e.g. `data`, `totalCount`, `currentPage`, `totalPages`, `hasNextPage`, `hasPrevPage`).

***

## GET /api/tokens/creator/:address

Get tokens created by a specific creator address.

**Path parameters:**

| Parameter | Type   | Description                                |
| --------- | ------ | ------------------------------------------ |
| `address` | string | Creator wallet address (0x + 40 hex chars) |

**Query parameters (all optional):**

| Parameter   | Type            | Description             |
| ----------- | --------------- | ----------------------- |
| `page`      | integer (min 1) | Page number             |
| `pageSize`  | integer (1–100) | Items per page          |
| `sortBy`    | string          | Same as GET /api/tokens |
| `sortOrder` | string          | `asc` or `desc`         |
| `chainId`   | integer (min 1) | Filter by chain ID      |

**Response:** Paginated list of tokens (e.g. `data`, `totalCount`, `currentPage`, `totalPages`).

***

## GET /api/tokens/address/:address

Get token details by token contract address.

**Path parameters:**

| Parameter | Type   | Description                                |
| --------- | ------ | ------------------------------------------ |
| `address` | string | Token contract address (0x + 40 hex chars) |

**Query parameters (optional):**

| Parameter | Type            | Description                                                           |
| --------- | --------------- | --------------------------------------------------------------------- |
| `chainId` | integer (min 1) | Chain ID (optional; used when same address exists on multiple chains) |

**Response:** Single token object (metadata, reserves, price, etc.).

***

## GET /api/tokens/address/:address/calc-buy-return

Calculate token amount received for a given ETH (or native token) amount (bonding curve buy).

**Path parameters:**

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `address` | string | Token contract address |

**Query parameters (required):**

| Parameter   | Type            | Description                             |
| ----------- | --------------- | --------------------------------------- |
| `ethAmount` | string          | ETH amount (human-readable, e.g. "0.1") |
| `chainId`   | integer (min 1) | Chain ID                                |

**Response:** `ethAmount`, `tokenAmount`, `tokenAmountFormatted`, `cached`, optional `needsSync`.

***

## GET /api/tokens/address/:address/calc-sell-return

Calculate ETH (or native token) amount received for a given token amount (bonding curve sell).

**Path parameters:**

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `address` | string | Token contract address |

**Query parameters (required):**

| Parameter     | Type            | Description                   |
| ------------- | --------------- | ----------------------------- |
| `tokenAmount` | string          | Token amount (human-readable) |
| `chainId`     | integer (min 1) | Chain ID                      |

**Response:** `tokenAmount`, `ethAmount`, `ethAmountFormatted`, `cached`, optional `needsSync`.

