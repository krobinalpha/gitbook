# Diagrams

These diagrams are intended to make the mechanics easy to visualize. They are conceptual and should match the deployed contract behavior.

## BondXCoin LP bootstrap (current design)

```mermaid
flowchart TD
  A[Trades happen on a chain] --> B[Buyback fee accumulates: accumulatedBuybackFee]
  B --> C{buybackLpAdded == false AND accumulatedBuybackFee >= BUYBACK_LP_THRESHOLD?}
  C -- No --> B
  C -- Yes --> D[Add BondXCoin/ETH liquidity on Uniswap using BUYBACK_LP_THRESHOLD]
  D --> E[Burn LP tokens]
  E --> F[Set buybackLpAdded=true and bondXCoinListed=true]
```

## Fee routing on buys/sells (high-level)

```mermaid
flowchart TD
  T[Trade (buy/sell)] --> F[Compute market-cap fee tier]
  F --> TR[Treasury fee]
  F --> CR[Creator fee]
  F --> BB[Buyback fee]
  TR --> TR2[Send to treasuryAddress + increment accumulator]
  CR --> CR2[Send to token creator]
  BB --> BB2[Accumulate; bootstrap LP once; then buyback+burn when thresholds are met]
```

## Buyback + burn (concept)

```mermaid
flowchart TD
  A[Trade] --> B[Buyback fee collected]
  B --> C[Swap ETH -> BONDX on Uniswap]
  C --> D[Burn BONDX received]
  D --> E[Supply reduction; potential buy pressure]
```

## BondXCoin LP bootstrap + LP burn (concept)

```mermaid
flowchart TD
  A[Buyback fee accumulation] --> B[When threshold reached, add liquidity (ETH + BondXCoin)]
  B --> C[Burn LP tokens]
  C --> D[BondXCoin liquidity can increase; buyback/burn can proceed later]
```


