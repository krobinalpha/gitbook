# Transparency & Analytics

BondX is designed to support “transparent by default” reporting.

## What can be verified on-chain
Examples include:

- total trading volume (`totalTradingVolume`)
- per-user trading volume (`userTradingVolume[address]`)
- points (`userPoints[address]`)
- tokens created by creator (`creatorTokens[address]`)
- accumulated fees (`accumulated*Fee`)
- phase state (`isPhase2Active`)
- LP listing threshold (`LP_LISTING_THRESHOLD`)

## Off-chain indexing (optional)
Event indexing can provide richer views (rankings, history, leaderboards) while remaining consistent with on-chain truth.

When off-chain metrics are displayed, BondX should clearly label:

- which chain the data refers to
- whether the metric is computed from on-chain reads or indexed events
- the time window (if applicable)


