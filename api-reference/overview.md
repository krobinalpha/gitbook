# 📡 API Reference

This section has three parts: **REST API**, **WebSocket (Socket.IO)**, and **On-chain events**. Use them to read and stream token data, trades, and to subscribe to contract events.

## For trading bots

* **REST API:** Poll token list, token details, calc buy/sell return, transactions, and price history. Use for polling-based strategies; always send `chainId` when the token exists on multiple chains. Pagination uses `page` and `pageSize`.
* **WebSocket:** Real-time trade and price events. Subscribe once; filter by `tokenAddress` and `chainId` in your client. Use for copy-trading, alerts, or low-latency signals.
* **On-chain events:** Subscribe to the BondX Pool contract (TokenBought, TokenSold, TokenCreated, TokenGraduated) via your own RPC/WebSocket provider for lowest latency and full independence from our servers.

***

## REST API

Public HTTP endpoints. Only endpoints that do not require authentication and are not admin-only are listed.

### Base URL

* **Production:** `https://bondx.fun` (or the BondX web app origin). All API paths are under `/api/` (e.g. `GET https://bondx.fun/api/tokens`).
* **Development:** `http://localhost:5000` (or your backend port). Same `/api/` prefix.

### Conventions

* **Content type:** Requests and responses are JSON (`Content-Type: application/json`).
* **Paths:** Documented paths are relative to the base URL (e.g. `GET /api/tokens` means `GET {baseUrl}/api/tokens`).
* **Path parameters** use `:param` (e.g. `:address`, `:tokenAddress`). Replace with actual values.
* **Query parameters** are optional unless marked required in the category pages.
* **Pagination:** List endpoints return `data`, `totalCount`, `currentPage`, `totalPages`, `hasNextPage`, `hasPrevPage`. Use `page` (min 1) and `pageSize` to control results.
* **Numeric fields:** Amounts in REST responses are human-readable strings unless a category page states otherwise (e.g. wei). Calc endpoints return both wei-style and formatted fields where relevant.
* **Rate limits:** Anonymous clients: 100 requests per minute (per IP). Authenticated clients: 200 requests per minute (per user). Exceeding limits returns HTTP 429.

### Scope

* **Included:** GET endpoints for public data (tokens, holders, histories, transactions, liquidity events, user profile, analytics rankings, platform stats, chat messages). Auth entry points: nonce, verify-wallet, send/verify email code, initiate social login.
* **Excluded:** All `/api/admin/*` routes; any endpoint that requires a Bearer token (e.g. `/auth/me`, profile update, wallet operations, token creation/buy/sell, upload, claim rewards); OAuth callback URLs; sitemap and other non-data APIs.

### REST categories

| Category                        | Description                                                                                          |
| ------------------------------- | ---------------------------------------------------------------------------------------------------- |
| [Tokens](tokens.md)             | List tokens, get token by address, tokens by creator, calc buy/sell return, user balance for a token |
| [Holders](holders.md)           | Token holders for a token; tokens held by an address; batch holder lookup                            |
| [Histories](histories.md)       | Price history for a token                                                                            |
| [Transactions](transactions.md) | Transactions for a token or for an address                                                           |
| [Liquidity](liquidity.md)       | Liquidity events for a token                                                                         |
| [Users](users.md)               | Public user profile by wallet address                                                                |
| [Auth](auth.md)                 | Nonce, verify wallet (SIWE), send/verify email code, initiate social login                           |
| [Analytics](analytics.md)       | Dashboard rankings (traders, points), platform stats                                                 |
| [Chat](chat.md)                 | List chat messages for a token                                                                       |

***

## WebSocket (Socket.IO)

Real-time events over Socket.IO. Only **unauthenticated** events are documented: price updates, trades, token created/traded, and chat (after joining a token room). Events that require an authenticated user room (deposit/withdraw/balance) are not documented.

See [**WebSocket**](websocket.md) for connection URL, client/server events, and payloads.

***

## On-chain events

BondX Pool contract emits **TokenBought**, **TokenSold**, **TokenCreated**, and **TokenGraduated**. You can subscribe via your own RPC or WebSocket provider (e.g. ethers `contract.on(...)`).

See [**On-chain events**](onchain-events.md) for contract address per chain, event names, and parameters.
