# ◽ Fees (Graduation Tiers)

BondX charges trading fees on **buys and sells**. Fees are expressed in basis points (BPS).

## BPS denominator

* `BPS_DENOMINATOR = 10,000`
* Example: `50 bps = 0.50%`

## Fee components (no LP fee)

Each trade computes three fees (in the chain’s **native token**, e.g. ETH/BNB):

* **Creator fee** → sent directly to the token creator
* **Treasury fee** → sent directly to `treasuryAddress` and tracked via `accumulatedTreasuryFee`
* **Buyback fee** → tracked via `accumulatedBuybackFee` and used for BondXCoin LP bootstrap + buyback/burn

## Fee tier selection (graduation-progress based)

BondX selects a fee tier based on the token’s **progress toward graduation**, using the token’s `realEthReserves` relative to its `graduationEth` target.

Tier thresholds are **percentages of `graduationEth`**:

* Tier 1: (0%) → (35%) of `graduationEth`
* Tier 2: (35%) → (70%) of `graduationEth`
* Tier 3: (70%) → (100%) of `graduationEth`
* Default: (\ge 100%) of `graduationEth` (same rates as Tier 3 in the current contract)

Equivalently, define:

* progress = `realEthReserves / graduationEth`

and select tiers by progress thresholds (0.35) and (0.70).

**Note on units:** `graduationEth` is a per-chain constant (e.g. **3 ETH** on ETH-like chains and **10 BNB** on BSC in the current codebase).

## Fee rates by tier

All tiers currently total **100 bps (1.0%)**, but the split changes:

### Tier 1 (progress < 35%)

* Creator: **30 bps** (0.30%)
* Treasury: **50 bps** (0.50%)
* Buyback: **20 bps** (0.20%)

### Tier 2 (35% ≤ progress < 70%)

* Creator: **40 bps** (0.40%)
* Treasury: **40 bps** (0.40%)
* Buyback: **20 bps** (0.20%)

### Tier 3 (70% ≤ progress < 100%)

* Creator: **60 bps** (0.60%)
* Treasury: **20 bps** (0.20%)
* Buyback: **20 bps** (0.20%)

## Notes

* Fees are computed on the trade’s **native token** amount and applied on-chain.
* Fee accounting is per-chain (each chain deployment is independent).
