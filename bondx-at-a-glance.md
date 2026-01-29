# ⚖️ BondX at a Glance

## What BondX is

A launchpad for creating and trading tokens through an on-chain bonding curve, with **graduation-progress fee tiers** and a **points/tier system** designed to reward participation.

## What makes BondX different

* **On-chain fee accounting**: the protocol tracks accumulated fees (treasury + buyback) on-chain.
* **Graduation-progress tiered fees**: fee split changes as a token moves toward graduation (no LP fee in the current design).
* **BondXCoin LP bootstrap**: buyback fee can fund a one-time BondXCoin/native-token liquidity bootstrap and then ongoing buyback+burn (execution depends on DEX conditions).
* **User incentives**: points and points-based tiers reward consistent participation, not only one-time events.

## Multi-chain model

BondX runs the same product experience across multiple chains, but each chain’s:

* contract deployment
* liquidity state
* fees and metrics

are **independent**.

## Key on-chain tracked metrics (per chain)

* **Total platform trading volume**: `totalTradingVolume`
* **Per-user trading volume**: `userTradingVolume[user]`
* **Per-user points**: `userPoints[user]`
* **Fee accumulators**: `accumulatedTreasuryFee`, `accumulatedBuybackFee`
* **BondXCoin LP bootstrap state**: `buybackLpAdded`, `bondXCoinListed`
* **Fee tier parameters**: `feeTier1/2/3/default`, `BPS_DENOMINATOR`, and the tier thresholds derived from `graduationEth`

## Fees (summary)

BondX uses basis points (BPS). Fees are **graduation-progress tiered** and split into:

* creator fee
* treasury fee
* buyback fee

All current tiers total **1.0%** (100 bps).
