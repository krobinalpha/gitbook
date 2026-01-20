# 💰 Treasury & Buyback Flows

BondX tracks and routes fee flows on-chain, per chain deployment.

## Key on-chain accumulators

- `accumulatedTreasuryFee`
- `accumulatedBuybackFee`

## Treasury fee

- Computed per trade via the current **graduation-progress fee tier**.
- Sent directly to `treasuryAddress`.
- Increments `accumulatedTreasuryFee` and emits `TreasuryFeePaid`.

## Creator fee

- Computed per trade via the current fee tier.
- Sent directly to the token creator and emits `CreatorFeePaid`.
- Not stored in an on-chain accumulator in the current contract.

## Buyback fee

- Computed per trade via the current fee tier.
- Increments `accumulatedBuybackFee`.
- Used for:
  - a one-time **BondXCoin LP bootstrap** on the configured UniswapV2-style router (when `BUYBACK_LP_THRESHOLD` is reached and `buybackLpAdded == false`), and then
  - **buyback + burn** operations when enough buyback native token accumulates (subject to `MIN_BUYBACK_AMOUNT`).

## “Accumulated” vs “executed”

Investors should distinguish between:

- **accumulated totals** (on-chain accounting variables), and
- **executed operations** (buyback swaps, liquidity adds), which can be subject to slippage, minimum thresholds, and execution failures.

Because key values are on-chain, dashboards can display fee totals without relying only on off-chain indexing.
