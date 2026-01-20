# ☸️ BondXCoin LP Bootstrap (Buyback Fee)

The current deployed BondX contract has **no Phase 1 / Phase 2** and **no LP fee**.

Instead, the protocol uses the **buyback fee** to:

1) bootstrap initial BondXCoin/native-token liquidity on the configured UniswapV2-style router, then  
2) perform ongoing buyback-and-burn operations when enough buyback native token accumulates.

## Key on-chain state

- `accumulatedBuybackFee` (ETH)
- `buybackLpAdded` (bool)
- `bondXCoinListed` (bool)

## Bootstrap threshold

From `BondX.sol`:

- `BUYBACK_LP_THRESHOLD` is **chain-specific**:
  - Ethereum / Arbitrum / Base: `5` (native token units, i.e. **5 ETH**)
  - BSC: `15` (native token units, i.e. **15 BNB**)
- `BUYBACK_LP_TOKEN_AMOUNT = 50,000,000 BondXCoin` (18 decimals)

## How it works (high level)

- On each trade, the buyback portion increases `accumulatedBuybackFee`.
- If `buybackLpAdded == false` and `accumulatedBuybackFee >= BUYBACK_LP_THRESHOLD`:
  - BondX attempts to add BondXCoin/native-token liquidity using exactly `BUYBACK_LP_THRESHOLD` worth of native token.
  - On success:
    - `accumulatedBuybackFee -= BUYBACK_LP_THRESHOLD`
    - `buybackLpAdded = true`
    - `bondXCoinListed = true`
    - any remaining `accumulatedBuybackFee` may be used for buyback/burn (subject to minimums)

## Minimum execution amounts

- `MIN_BUYBACK_AMOUNT = 0.01 ETH`
- `MIN_LP_ADD_AMOUNT = 0.01 ETH`

## What users should expect

- Before LP bootstrap succeeds, buyback native token accumulates.
- After LP bootstrap, buyback/burn can execute when enough ETH is accumulated.
- These mechanics do not guarantee market outcomes; swaps can fail due to liquidity, slippage, or routing.
