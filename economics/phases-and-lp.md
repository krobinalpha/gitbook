# ☸️ BondXCoin LP Bootstrap (Buyback Fee)

The current deployed BondX contract has **no Phase 1 / Phase 2** and **no LP fee**.

Instead, the protocol uses the **buyback fee** to:

1) bootstrap initial BondXCoin/ETH liquidity on Uniswap, then  
2) perform ongoing buyback-and-burn operations when enough buyback ETH accumulates.

## Key on-chain state

- `accumulatedBuybackFee` (ETH)
- `buybackLpAdded` (bool)
- `bondXCoinListed` (bool)

## Bootstrap threshold

From `BondX.sol`:

- `BUYBACK_LP_THRESHOLD = 5 ETH`
- `BUYBACK_LP_TOKEN_AMOUNT = 50,000,000 BondXCoin` (18 decimals)

## How it works (high level)

- On each trade, the buyback portion increases `accumulatedBuybackFee`.
- If `buybackLpAdded == false` and `accumulatedBuybackFee >= BUYBACK_LP_THRESHOLD`:
  - BondX attempts to add BondXCoin/ETH liquidity using exactly `BUYBACK_LP_THRESHOLD` worth of ETH.
  - On success:
    - `accumulatedBuybackFee -= BUYBACK_LP_THRESHOLD`
    - `buybackLpAdded = true`
    - `bondXCoinListed = true`
    - any remaining `accumulatedBuybackFee` may be used for buyback/burn (subject to minimums)

## Minimum execution amounts

- `MIN_BUYBACK_AMOUNT = 0.01 ETH`
- `MIN_LP_ADD_AMOUNT = 0.01 ETH`

## What users should expect

- Before LP bootstrap succeeds, buyback ETH accumulates.
- After LP bootstrap, buyback/burn can execute when enough ETH is accumulated.
- These mechanics do not guarantee market outcomes; swaps can fail due to liquidity, slippage, or routing.
