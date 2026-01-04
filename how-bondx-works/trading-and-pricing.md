# Trading & Pricing

BondX maintains internal reserve-like state for each token, updating virtual and real reserves on buys/sells.

This design allows BondX to:

- quote prices deterministically from on-chain state
- track volume on-chain
- apply phase-based fees consistently

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

## Points note
In the current on-chain design, **buys award points** while **sells do not** (this helps avoid certain self-trading reward loops).


