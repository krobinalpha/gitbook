# ⬜ Transparency & Analytics

BondX is designed to support “transparent by default” reporting.

## What can be verified on-chain

Examples include:

* total trading volume (`totalTradingVolume`)
* per-user trading volume (`userTradingVolume[address]`)
* points (`userPoints[address]`)
* tokens created by creator (`creatorTokens[address]`)
* accumulated fees (`accumulated*Fee`)
* phase state (`isPhase2Active`)
* LP listing threshold (`LP_LISTING_THRESHOLD`)

## Off-chain indexing (optional)

Event indexing can provide richer views (rankings, history, leaderboards) while remaining consistent with on-chain truth.

When off-chain metrics are displayed, BondX should clearly label:

<<<<<<< HEAD
- which chain the data refers to
- whether the metric is computed from on-chain reads or indexed events
- the time window (if applicable)

## Recommended metric definitions (for dashboards)

To avoid confusion, dashboards should define metrics precisely:

- **Total Platform Volume (ETH)**: `totalTradingVolume` on the selected chain.
- **Treasury Fee (ETH)**: `accumulatedTreasuryFee` on the selected chain.
- **LP Fee (ETH)**: `accumulatedLPFee` on the selected chain.
- **Buyback Fee (ETH)**: `accumulatedBuybackFee` on the selected chain.
- **User Tier**: derived from `userTradingVolume[user]` vs tier thresholds (per chain).
- **Creator tokens created**: count of `creatorTokens[creator]` (per chain deployment).

## Fast + correct rankings (best practice)

Rankings should be:

- **chain-specific**
- computed from a consistent data source (on-chain reads and/or indexed events)
- cached with clear refresh semantics (e.g., update every N minutes)



=======
* which chain the data refers to
* whether the metric is computed from on-chain reads or indexed events
* the time window (if applicable)
>>>>>>> f3332b51e1054aeb4b6b935a87abd65205368d67
