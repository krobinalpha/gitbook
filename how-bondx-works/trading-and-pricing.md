# Trading & Pricing

BondX maintains internal reserve-like state for each token, updating virtual and real reserves on buys/sells.

## Buys

- Buyer sends native token (ETH on EVM chains).
- Contract calculates token output and applies phase-based fees.
- Contract transfers tokens to the buyer.

## Sells

- Seller sends tokens to the contract.
- Contract calculates ETH output and applies phase-based fees.
- Contract transfers net ETH to the seller.

## Platform-wide volume
The contract tracks:

- per-user trading volume
- total trading volume across all users

This enables transparency around usage and participation.


