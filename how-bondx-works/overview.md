# 🚟 How BondX Works

BondX is an on-chain system that supports:

* token creation
* trading activity (buy/sell)
* fee collection and accounting
* phase tracking
* points and tier bonuses

At a high level:

1. A creator deploys a new token through the BondX contract.
2. Traders buy/sell; the contract applies phase-based fees.
3. The contract tracks accumulated fees on-chain.
4. A phase transition can occur once LP listing conditions are met.
5. Users earn points and tier bonuses based on rules defined in the contract.

## “Source of truth”

For any chain, the primary source of truth is the BondX contract on that chain. Off-chain analytics can improve UX, but should remain consistent with:

* on-chain accumulators (fees)
* on-chain volume (per user and total)
* on-chain points and claimable rewards
