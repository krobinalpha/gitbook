# ⛓️ On-chain events

The BondX Pool contract (BondxPool) emits events for buys, sells, token creation, and graduation. You can subscribe via your own RPC or WebSocket provider for lowest latency and full independence from our servers.

## For trading bots

Subscribe to the BondX Pool contract (TokenBought, TokenSold, TokenCreated, TokenGraduated) using your own node or provider. Events fire when the block is mined; consider waiting for confirmations before treating a trade as final. All amount parameters are **wei** (uint256). The full ABI is in the repo at `backend/src/config/abi/BondxPool.json`; only the four events below are documented here.

## Contract

* **Contract:** BondX Pool (BondxPool). One deployment per chain.
* **Supported chain IDs:** 1 (Ethereum), 56 (BSC), 42161 (Arbitrum), 8453 (Base), 84532 (Base Sepolia).
* **Address per chain:** Pool address is deployment-specific. Obtain it from the BondX app, docs, or a public API if available. The backend uses `POOL_ADDRESS_*` environment variables; the same addresses are used for indexing and WebSocket emissions.

***

## TokenBought

Emitted when a user buys tokens (bonding curve buy).

| Parameter                 | Indexed | Type    | Description                        |
| ------------------------- | ------- | ------- | ---------------------------------- |
| `tokenAddress`            | yes     | address | Token contract address             |
| `buyer`                   | yes     | address | Buyer wallet address               |
| `ethAmount`               | no      | uint256 | Native token amount (wei)          |
| `tokenAmount`             | no      | uint256 | Token amount received (wei)        |
| `newEthReserves`          | no      | uint256 | Pool ETH reserves after trade      |
| `newTokenReserves`        | no      | uint256 | Pool token reserves after trade    |
| `newVirtualEthReserves`   | no      | uint256 | Virtual ETH reserves after trade   |
| `newVirtualTokenReserves` | no      | uint256 | Virtual token reserves after trade |

***

## TokenSold

Emitted when a user sells tokens (bonding curve sell).

| Parameter                 | Indexed | Type    | Description                        |
| ------------------------- | ------- | ------- | ---------------------------------- |
| `tokenAddress`            | yes     | address | Token contract address             |
| `seller`                  | yes     | address | Seller wallet address              |
| `tokenAmount`             | no      | uint256 | Token amount sold (wei)            |
| `ethAmount`               | no      | uint256 | Native token amount received (wei) |
| `newEthReserves`          | no      | uint256 | Pool ETH reserves after trade      |
| `newTokenReserves`        | no      | uint256 | Pool token reserves after trade    |
| `newVirtualEthReserves`   | no      | uint256 | Virtual ETH reserves after trade   |
| `newVirtualTokenReserves` | no      | uint256 | Virtual token reserves after trade |

***

## TokenCreated

Emitted when a new token is created on the BondX pool.

| Parameter              | Indexed | Type    | Description                                |
| ---------------------- | ------- | ------- | ------------------------------------------ |
| `tokenAddress`         | yes     | address | New token contract address                 |
| `creator`              | yes     | address | Creator wallet address                     |
| `name`                 | no      | string  | Token name                                 |
| `symbol`               | no      | string  | Token symbol                               |
| `description`          | no      | string  | Token description                          |
| `uri`                  | no      | string  | Metadata URI                               |
| `totalSupply`          | no      | uint256 | Total supply (wei)                         |
| `virtualEthReserves`   | no      | uint256 | Initial virtual ETH reserves               |
| `virtualTokenReserves` | no      | uint256 | Initial virtual token reserves             |
| `graduationEth`        | no      | uint256 | Graduation threshold in native token (wei) |

***

## TokenGraduated

Emitted when a token reaches its graduation threshold (bonding curve graduates to LP).

| Parameter         | Indexed | Type    | Description               |
| ----------------- | ------- | ------- | ------------------------- |
| `tokenAddress`    | yes     | address | Token contract address    |
| `graduationPrice` | no      | uint256 | Price at graduation (wei) |

***

## Subscription

Subscribe using your own RPC or WebSocket provider. Example with ethers.js v6:

```javascript
const { ethers } = require('ethers');

const POOL_ADDRESS = '0x...'; // BondX Pool address for the chain
const RPC_URL = 'https://...';
const provider = new ethers.JsonRpcProvider(RPC_URL);

const abi = [
  'event TokenBought(address indexed tokenAddress, address indexed buyer, uint256 ethAmount, uint256 tokenAmount, uint256 newEthReserves, uint256 newTokenReserves, uint256 newVirtualEthReserves, uint256 newVirtualTokenReserves)',
  'event TokenSold(address indexed tokenAddress, address indexed seller, uint256 tokenAmount, uint256 ethAmount, uint256 newEthReserves, uint256 newTokenReserves, uint256 newVirtualEthReserves, uint256 newVirtualTokenReserves)',
];

const contract = new ethers.Contract(POOL_ADDRESS, abi, provider);

contract.on('TokenBought', (tokenAddress, buyer, ethAmount, tokenAmount, newEthReserves, newTokenReserves, newVirtualEthReserves, newVirtualTokenReserves, event) => {
  console.log('TokenBought', tokenAddress, buyer, ethAmount.toString(), tokenAmount.toString(), event.log.transactionHash);
});

contract.on('TokenSold', (tokenAddress, seller, tokenAmount, ethAmount, newEthReserves, newTokenReserves, newVirtualEthReserves, newVirtualTokenReserves, event) => {
  console.log('TokenSold', tokenAddress, seller, tokenAmount.toString(), ethAmount.toString(), event.log.transactionHash);
});
```

Replace `POOL_ADDRESS` and `RPC_URL` with the BondX Pool address and RPC for your target chain. Callbacks receive event args and an event object (e.g. `event.log.transactionHash`, `event.log.blockNumber`). The backend subscribes to these same events to index and emit Socket.IO; your subscription is independent and can run from any provider that supports `eth_subscribe` (logs).
