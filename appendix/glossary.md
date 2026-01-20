# Glossary

## BPS (basis points)
One basis point is 0.01%. 100 bps = 1%.

## Chain-specific economics
BondX runs independent deployments per chain. Volume, fees, phase state, and rankings are per chain.

## Fee tier (graduation-progress based)
BondX selects a fee split based on the token’s graduation progress (its `realEthReserves` relative to `graduationEth`). Tiers are defined by `feeTier1/2/3/default` structs and the progress thresholds derived from `graduationEth` (35% and 70% in the current contract).

## Buyback fee
Fee portion accumulated on-chain and used for BondXCoin LP bootstrap and buyback+burn operations (execution depends on thresholds and DEX conditions).

## Buyback LP bootstrap
One-time liquidity add funded by accumulated buyback fees once `BUYBACK_LP_THRESHOLD` is reached (sets `buybackLpAdded = true`).

## Treasury fee
Fee portion sent to a treasury address and also tracked via an on-chain accumulator.

## Points
On-chain score earned from actions (create, buy activity, progress). Intended to be redeemable for BONDX rewards.

## Tier
Volume-based classification (Bronze → Mythic) based on total trading volume on a chain.


