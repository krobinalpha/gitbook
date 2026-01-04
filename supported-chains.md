# Supported Chains

BondX is a multi-chain launchpad. Current supported chains:

- **Ethereum**
- **Arbitrum**
- **Base**

More chains may be added later.

## Important: per-chain independence
Each chain has its own independent BondX deployment. This means:

- platform volume is per-chain
- fees accumulate per-chain
- phase state is per-chain
- liquidity state is per-chain

BondX may present a unified UX, but **economics do not mix across chains**.

## Practical implication for users

When a user switches chain, all of the following are chain-specific:

- platform volume and rankings
- treasury/LP/buyback accumulators
- whether Phase 2 is active
- reward claiming availability (in the current contract design)



