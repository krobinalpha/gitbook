# Treasury, LP & Buyback Flows

BondX tracks fee accumulation on-chain, per chain.

## Key on-chain accumulators

- `accumulatedTreasuryFee`
- `accumulatedLPFee`
- `accumulatedBuybackFee`

## Treasury fee

- Taken on buys/sells using the phase-based treasury bps.
- Sent directly to the configured `treasuryAddress`.
- Also increments `accumulatedTreasuryFee`.

## LP fee

- Phase 1: LP fee accumulates into `accumulatedLPFee`.
- Phase 2: LP fee can be used for liquidity operations, with minimum execution thresholds enforced.

## Buyback fee

- Phase 1: set to 0 bps (effectively no buyback fee).
- Phase 2: buyback fee is enabled; it may execute immediately and/or accumulate based on minimum thresholds and execution outcomes.

## “Accumulated” vs “executed”

Investors should distinguish between:

- **accumulated fee totals** (on-chain accounting variables), and
- **executed operations** (e.g., buyback swaps, liquidity adds), which can be subject to slippage, minimum thresholds, and execution failures.

BondX tracks both accounting and execution events, enabling transparency around “what should have happened” vs “what actually happened”.

## Why this matters for transparency
Because these values are on-chain, analytics dashboards can show fee totals without relying solely on off-chain indexing.


