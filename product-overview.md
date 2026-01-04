# 🧩 Product Overview

BondX is a multi-chain launchpad that supports:

* token creation by creators
* early buy/sell trading by users
* phase-based fee routing (Phase 1 vs Phase 2)
* a points + tier system that rewards activity and progress

## Core design principles

### Transparency by default
If a metric matters to users (fees, volume, phase, rewards), it should be either:

* directly verifiable on-chain, or
* derived from indexed events with clear definitions and chain IDs

### Per-chain independence
Each chain has:

* its own BondX deployment
* its own BONDX liquidity state
* its own phase progression
* its own fee accumulators and totals

This prevents “accounting confusion” and keeps incentives clean.

### UX: one experience, many chains
BondX can present a single product UX while still respecting the reality that each chain is its own market.


