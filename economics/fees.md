# ◽ Fees (Market Cap Tiers)

BondX charges trading fees on **buys and sells**. Fees are expressed in basis points (BPS).

## BPS denominator

- `BPS_DENOMINATOR = 10,000`
- Example: `50 bps = 0.50%`

## Fee components (no LP fee)

Each trade computes three fees (in ETH):

- **Creator fee** → sent directly to the token creator
- **Treasury fee** → sent directly to `treasuryAddress` and tracked via `accumulatedTreasuryFee`
- **Buyback fee** → tracked via `accumulatedBuybackFee` and used for BondXCoin LP bootstrap + buyback/burn

## Fee tier selection (market cap based)

BondX selects a fee tier based on the token’s **current market cap**:

- `calculateMarketCap(token)` = `(virtualEthReserves / virtualTokenReserves) * totalSupply`

Tier caps (ETH):

- `FEE_TIER1_CAP = 6 ETH`
- `FEE_TIER2_CAP = 10 ETH`
- `FEE_TIER3_CAP = 16 ETH`
- `feeTierDefault` applies when `marketCap >= 16 ETH`

## Fee rates by tier

All tiers currently total **100 bps (1.0%)**, but the split changes:

### Tier 1 (market cap < 6 ETH)

- Creator: **30 bps** (0.30%)
- Treasury: **50 bps** (0.50%)
- Buyback: **20 bps** (0.20%)

### Tier 2 (6 ETH ≤ market cap < 10 ETH)

- Creator: **40 bps** (0.40%)
- Treasury: **40 bps** (0.40%)
- Buyback: **20 bps** (0.20%)

### Tier 3 (10 ETH ≤ market cap < 16 ETH)

- Creator: **60 bps** (0.60%)
- Treasury: **20 bps** (0.20%)
- Buyback: **20 bps** (0.20%)

### Default (market cap ≥ 16 ETH)

- Same as Tier 3 (current contract)

## Notes

- Fees are computed on the trade’s ETH amount and applied on-chain.
- Fee accounting is per-chain (each chain deployment is independent).
