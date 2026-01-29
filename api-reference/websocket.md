# WebSocket (Socket.IO)

Real-time events over Socket.IO. Only events that **do not require authentication** are documented. Authentication is optional; without it, clients still receive all events listed below.

## For trading bots

Listen to `tokenBought`, `tokenSold`, and optionally `priceUpdate`, `tokenCreated`, `tokenTraded`. Events are **broadcast for all tokens**; filter by `tokenAddress` and `chainId` in your client. Chat events (`chatMessage`, `chatMessageEdited`, `chatMessageDeleted`) are for the app; most bots ignore them. Use a **Socket.IO client** (not raw WebSocket). Socket.IO handles reconnection; keep it enabled.

## Connection

- **URL:** `wss://bondx.fun/socket.io/` (production; use your BondX app origin). Same host as the web app; path `/socket.io/`.
- **Client:** Socket.IO client (e.g. `socket.io-client`). Connect with or without an auth token; public events are broadcast to all connected clients. Reconnection is built-in; enable it for long-lived bots.

### Example (Node.js)

```javascript
const { io } = require('socket.io-client');

const socket = io('https://bondx.fun', {
  path: '/socket.io/',
  transports: ['websocket', 'polling'],
  reconnection: true,
});

const TARGET_TOKEN = '0x...'; // lowercase
const TARGET_CHAIN_ID = 8453;

socket.on('tokenBought', (data) => {
  if (data.tokenAddress !== TARGET_TOKEN || data.chainId !== TARGET_CHAIN_ID) return;
  console.log('Buy', data.txHash, data.ethAmount, data.tokenAmount, data.tokenPrice);
});

socket.on('tokenSold', (data) => {
  if (data.tokenAddress !== TARGET_TOKEN || data.chainId !== TARGET_CHAIN_ID) return;
  console.log('Sell', data.txHash, data.ethAmount, data.tokenAmount, data.tokenPrice);
});

socket.on('connect', () => console.log('Connected'));
socket.on('connect_error', (err) => console.error('Connection error', err));
```

## Client to Server (optional)

| Event | Description |
|-------|-------------|
| `joinTokenChat` | Emit with token address (lowercase string) to subscribe to chat events for that token. You will receive `chatMessage`, `chatMessageEdited`, `chatMessageDeleted` for this token. |
| `leaveTokenChat` | Emit with token address (lowercase string) to unsubscribe from that token's chat room. |

## Server to Client events (no auth required)

All events below are emitted to all connected clients (or to the token chat room for chat events). No Bearer token or user room required.

**Numeric types:** In `tokenBought`, `tokenSold`, and `tokenTraded`, `ethAmount`, `tokenAmount`, and `value` are **wei strings** (18 decimals). Convert with your library's `formatUnits` (or equivalent). `tokenPrice` and `price` in `priceUpdate` are human-readable strings.

### priceUpdate

Emitted when a token's price is updated (e.g. after a trade).

| Field | Type | Description |
|-------|------|-------------|
| `tokenAddress` | string | Token contract address (lowercase) |
| `price` | string | Price in native token (human-readable) |
| `priceUSD` | string | Price in USD (human-readable) |
| `timestamp` | string | ISO 8601 timestamp |
| `chainId` | number | Chain ID |

---

### tokenBought

Emitted when a buy trade is processed on-chain.

| Field | Type | Description |
|-------|------|-------------|
| `tokenAddress` | string | Token contract address |
| `buyer` | string | Buyer wallet address |
| `ethAmount` | string | Native token amount (wei string; 18 decimals) |
| `tokenAmount` | string | Token amount received (wei string; 18 decimals) |
| `txHash` | string | Transaction hash |
| `blockNumber` | number | Block number |
| `blockTimestamp` | string | ISO 8601 timestamp |
| `chainId` | number | Chain ID |
| `tokenPrice` | string | Token price after trade (human-readable) |
| `marketCap` | string | Market cap (human-readable) |
| `graduationProgress` | string | Graduation progress |
| `holders` | array | Updated holder list: `owner_address`, `balance`, `balanceUSD`, `percentage` |

---

### tokenSold

Emitted when a sell trade is processed on-chain.

| Field | Type | Description |
|-------|------|-------------|
| `tokenAddress` | string | Token contract address |
| `seller` | string | Seller wallet address |
| `ethAmount` | string | Native token amount received (wei string; 18 decimals) |
| `tokenAmount` | string | Token amount sold (wei string; 18 decimals) |
| `txHash` | string | Transaction hash |
| `blockNumber` | number | Block number |
| `blockTimestamp` | string | ISO 8601 timestamp |
| `chainId` | number | Chain ID |
| `tokenPrice` | string | Token price after trade (human-readable) |
| `marketCap` | string | Market cap (human-readable) |
| `graduationProgress` | string | Graduation progress |
| `holders` | array | Updated holder list |

---

### tokenCreated

Emitted when a new token is created on the platform.

| Field | Type | Description |
|-------|------|-------------|
| `tokenAddress` | string | Token contract address |
| `creatorAddress` | string | Creator wallet address |
| `name` | string | Token name |
| `symbol` | string | Token symbol |
| `description` | string | Description |
| `logo` | string | Logo URL |
| `totalSupply` | string | Total supply |
| `chainId` | number | Chain ID |
| `tokenPrice` | string | Initial token price |
| `marketCap` | string | Market cap (optional) |
| `holders` | array | Initial holders (optional) |
| `timestamp` | string | ISO 8601 timestamp |

---

### tokenTraded

Emitted when a direct transfer of the token occurs (not a buy/sell through the bonding curve).

| Field | Type | Description |
|-------|------|-------------|
| `tokenAddress` | string | Token contract address |
| `from` | string | Sender address |
| `to` | string | Recipient address |
| `value` | string | Transfer amount (wei string; 18 decimals) |
| `txHash` | string | Transaction hash |
| `blockNumber` | number | Block number |
| `blockTimestamp` | string | ISO 8601 timestamp |
| `chainId` | number | Chain ID |
| `tokenPrice` | string | Token price (human-readable) |
| `marketCap` | string | Market cap (human-readable) |
| `holders` | array | Updated holder list |

---

### chatMessage

Emitted when a new chat message is posted for a token. Only received if you have emitted `joinTokenChat` for that token.

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Message ID |
| `user` | string | Sender wallet address |
| `token` | string | Token address (chat room) |
| `message` | string | Message text |
| `reply_to` | string \| null | Reply target message ID (if any) |
| `timestamp` | string | ISO 8601 timestamp |
| `editedAt` | string \| null | Edit timestamp (optional) |

---

### chatMessageEdited

Emitted when a chat message is edited. Only received if you have joined that token's chat room.

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Message ID |
| `user` | string | Sender wallet address |
| `token` | string | Token address |
| `message` | string | Updated message text |
| `reply_to` | string \| null | Reply target message ID |
| `timestamp` | string | ISO 8601 timestamp |
| `editedAt` | string \| null | Edit timestamp |

---

### chatMessageDeleted

Emitted when a chat message is deleted. Only received if you have joined that token's chat room.

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Message ID |
| `token` | string | Token address |

---

## Out of scope (not documented)

The following are **not** documented in this reference because they require an authenticated user room or auth-only client actions:

- **Server events:** `depositDetected`, `withdrawDetected`, `balanceUpdate` (emitted only to `user:{userId}`).
- **Client event:** `chat:send` (sending a chat message requires a valid Bearer token).
