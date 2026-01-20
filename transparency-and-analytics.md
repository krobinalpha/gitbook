# ⬜ Transparency & Analytics

BondX is designed to support “transparent by default” reporting.

## What can be verified on-chain

Examples include:

* total trading volume (`totalTradingVolume`)
* per-user trading volume (`userTradingVolume[address]`)
* points (`userPoints[address]`)
* tokens created by creator (`creatorTokens[address]`)
* accumulated fees (`accumulatedTreasuryFee`, `accumulatedBuybackFee`)
* fee tier parameters (`feeTier1/2/3/default`, `BPS_DENOMINATOR`, and tier thresholds derived from `graduationEth`)
* BondXCoin / buyback state (`bondXCoinAddress`, `bondXCoinListed`, `buybackLpAdded`)
* buyback/LP bootstrap parameters (`BUYBACK_LP_THRESHOLD`, `MIN_BUYBACK_AMOUNT`, `MIN_LP_ADD_AMOUNT`)

## Off-chain indexing (optional)

Event indexing can provide richer views (rankings, history, leaderboards) while remaining consistent with on-chain truth.

When off-chain metrics are displayed, BondX should clearly label:

* which chain the data refers to
* whether the metric is computed from on-chain reads or indexed events
* the time window (if applicable)

## Recommended metric definitions (for dashboards)

To avoid confusion, dashboards should define metrics precisely:

* **Total Platform Volume (native token)**: `totalTradingVolume` on the selected chain (ETH/BNB).
* **Treasury Fees (native token)**: `accumulatedTreasuryFee` on the selected chain.
* **Buyback Fees (native token)**: `accumulatedBuybackFee` on the selected chain.
* **User Tier**: derived from `userPoints[user]` vs the points-tier thresholds (per chain leaderboards/ranks should also be chain-specific).
* **Creator tokens created**: count of `creatorTokens[creator]` (per chain deployment).

## Fast + correct rankings (best practice)

Rankings should be:

* **chain-specific**
* computed from a consistent data source (on-chain reads and/or indexed events)
* cached with clear refresh semantics (e.g., update every N minutes)
