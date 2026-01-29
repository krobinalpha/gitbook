# On-chain events

The BondX Pool contract (BondxPool) emits events for buys, sells, token creation, and graduation. You can subscribe to these events via your own RPC or WebSocket provider (e.g. ethers `contract.on(...)` or provider log filters).

## Contract

- **Contract:** BondX Pool (BondxPool). One deployment per chain; the pool address is deployment-specific (e.g. from env `POOL_ADDRESS_ETHEREUM`, `POOL_ADDRESS_BSC`, etc.).
- **Supported chain IDs:** 1 (Ethereum), 56 (BSC), 42161 (Arbitrum), 8453 (Base), 84532 (Base Sepolia).
- **Address per chain:** Obtain the pool contract address for each chain from the BondX app, docs, or API. The backend uses `POOL_ADDRESS_*` environment variables; the same addresses are used for indexing and WebSocket emissions.

The full ABI is in the backend at `backend/src/config/abi/BondxPool.json`. Only the four events below are documented here.

---

## TokenBought

Emitted when a user buys tokens (bonding curve buy).

| Parameter | Indexed | Type | Description |
|-----------|---------|------|-------------|
| `tokenAddress` | yes | address | Token contract address |
| `buyer` | yes | address | Buyer wallet address |
| `ethAmount` | no | uint256 | Native token amount (wei) |
| `tokenAmount` | no | uint256 | Token amount received (wei) |
| `newEthReserves` | no | uint256 | Pool ETH reserves after trade |
| `newTokenReserves` | no | uint256 | Pool token reserves after trade |
| `newVirtualEthReserves` | no | uint256 | Virtual ETH reserves after trade |
| `newVirtualTokenReserves` | no | uint256 | Virtual token reserves after trade |

---

## TokenSold

Emitted when a user sells tokens (bonding curve sell).

| Parameter | Indexed | Type | Description |
|-----------|---------|------|-------------|
| `tokenAddress` | yes | address | Token contract address |
| `seller` | yes | address | Seller wallet address |
| `tokenAmount` | no | uint256 | Token amount sold (wei) |
| `ethAmount` | no | uint256 | Native token amount received (wei) |
| `newEthReserves` | no | uint256 | Pool ETH reserves after trade |
| `newTokenReserves` | no | uint256 | Pool token reserves after trade |
| `newVirtualEthReserves` | no | uint256 | Virtual ETH reserves after trade |
| `newVirtualTokenReserves` | no | uint256 | Virtual token reserves after trade |

---

## TokenCreated

Emitted when a new token is created on the BondX pool.

| Parameter | Indexed | Type | Description |
|-----------|---------|------|-------------|
| `tokenAddress` | yes | address | New token contract address |
| `creator` | yes | address | Creator wallet address |
| `name` | no | string | Token name |
| `symbol` | no | string | Token symbol |
| `description` | no | string | Token description |
| `uri` | no | string | Metadata URI |
| `totalSupply` | no | uint256 | Total supply (wei) |
| `virtualEthReserves` | no | uint256 | Initial virtual ETH reserves |
| `virtualTokenReserves` | no | uint256 | Initial virtual token reserves |
| `graduationEth` | no | uint256 | Graduation threshold in native token (wei) |

---

## TokenGraduated

Emitted when a token reaches its graduation threshold (bonding curve graduates to LP).

| Parameter | Indexed | Type | Description |
|-----------|---------|------|-------------|
| `tokenAddress` | yes | address | Token contract address |
| `graduationPrice` | no | uint256 | Price at graduation (wei) |

---

## Subscription

Subscribe using your own RPC or WebSocket provider. Example with ethers.js:

1. Get the BondX Pool contract address for the desired chain.
2. Load the BondxPool ABI (or the event fragments for TokenBought, TokenSold, TokenCreated, TokenGraduated).
3. Create a contract instance with `new ethers.Contract(poolAddress, abi, provider)`.
4. Use `contract.on('TokenBought', callback)`, `contract.on('TokenSold', callback)`, etc. Callbacks receive the event arguments and optionally the event log (txHash, blockNumber, etc.).

The backend uses a WebSocket provider per chain and subscribes to these same events to update the database and emit Socket.IO events; your subscription is independent and can run from any node or provider that supports `eth_subscribe` (logs) or equivalent.
