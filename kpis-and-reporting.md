# 📊 KPIs & Reporting Standards

This section defines product-level KPIs and how BondX should report them professionally.

## Principles

* **Chain-specific first**: every KPI must specify the chain ID (Ethereum / Arbitrum / Base).
* **Clear source labeling**: each KPI must state whether it is:
  * on-chain direct read, or
  * derived from indexed events / database.
* **Time window clarity**: “24h / 7d / 30d / all-time” must be explicit.
* **Idempotent tracking**: event-based KPIs must guarantee no duplicate counting (txHash + chainId uniqueness).

## Core product KPIs (recommended)

### Adoption

* **Active users (daily/weekly)**: unique wallets that executed at least 1 buy/sell on the selected chain in the time window.
* **New creators**: unique creator addresses that created at least 1 token in the time window.
* **Tokens created**: count of token creation events on the selected chain (time window).

### Activity & Liquidity

* **Total platform volume (ETH)**: on-chain `totalTradingVolume` on the selected chain (all-time) + optional “period volume” from events.
* **Trades count**: number of buy/sell events in the time window (indexed).
* **Graduation rate**: % of tokens reaching graduation conditions (definition must match contract semantics).
* **BondXCoin LP bootstrap status**: `buybackLpAdded` and `bondXCoinListed` (per chain).

### Unit economics (transparent by design)

* **Treasury fee accumulated (ETH)**: on-chain `accumulatedTreasuryFee` on the selected chain (all-time).
* **Buyback fee accumulated (ETH)**: on-chain `accumulatedBuybackFee` on the selected chain (all-time).
* **Executed operations** (indexed from events):
  * buyback attempts, successes, failures
  * liquidity add attempts, successes, failures

### Rewards & incentives

* **Points issued**: on-chain `totalPointsDistributed` (per chain deployment).
* **Rewards distributed**: on-chain `totalRewardsDistributed` (per chain deployment).
* **Claiming enabled**: `isClaimingEnabled()` (per chain deployment).

## Reporting standard (what “professional” looks like)

For each KPI, dashboards and reports should include:

* definition (1 sentence)
* chain ID
* time window
* source (on-chain vs indexed)
* last updated time

This prevents confusion and increases investor trust.


