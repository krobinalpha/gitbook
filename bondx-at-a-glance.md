# ⚖️ BondX at a Glance

## What it is

A launchpad for creating and trading tokens, with phase-based fee routing and a points/tier system designed to reward participation.

## What makes it different

* **On-chain fee accounting**: the protocol tracks accumulated fees (LP / buyback / treasury) on-chain.
* **Phase-based behavior**: Phase 1 focuses on growth and LP accumulation; Phase 2 shifts fee routing and enables buyback and LP operations.
* **User incentives**: points and volume tiers reward consistent participation, not only one-time events.

## Multi-chain model

BondX runs the same product experience across multiple chains, but each chain’s:

* contract deployment
* liquidity state
* phases
* fees and metrics

are **independent**.
<<<<<<< HEAD

## Key on-chain tracked metrics (per chain)

- **Total platform trading volume**: `totalTradingVolume`
- **Per-user trading volume**: `userTradingVolume[user]`
- **Per-user points**: `userPoints[user]`
- **Fee accumulators**: `accumulatedTreasuryFee`, `accumulatedLPFee`, `accumulatedBuybackFee`
- **Phase state**: `isPhase2Active`

## Fees (summary)

BondX uses basis points (BPS). Fee schedules are phase-dependent:

- **Phase 1 total fee**: 3.0% (0.5% treasury + 2.5% LP + 0% buyback)
- **Phase 2 total fee**: 1.5% (0.3% treasury + 0.5% LP + 0.7% buyback)

The intent is to allow Phase 1 to emphasize growth and distribution incentives, then shift Phase 2 toward lower fees and sustainable operations.


=======
>>>>>>> f3332b51e1054aeb4b6b935a87abd65205368d67
