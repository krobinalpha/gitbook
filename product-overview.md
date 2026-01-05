# 🧩 Product Overview

BondX is a multi-chain launchpad that supports:

* token creation by creators
* early buy/sell trading by users
* market-cap tiered fees (creator + treasury + buyback; no LP fee)
* a points + tier system that rewards activity and progress
* embedded wallet withdrawals protected by **email OTP**

## Core design principles

### Transparency by default
If a metric matters to users (fees, volume, rewards), it should be either:

* directly verifiable on-chain, or
* derived from indexed events with clear definitions and chain IDs

### Per-chain independence
Each chain has:

* its own BondX deployment
* its own BONDX liquidity state
* its own fee accumulators and totals

This prevents “accounting confusion” and keeps incentives clean.

### UX: one experience, many chains
BondX can present a single product UX while still respecting the reality that each chain is its own market.


