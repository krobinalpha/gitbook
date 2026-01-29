# 🔤 Points & User Tiers

BondX includes an on-chain points system and a points-based tier structure.

Points and tiers are designed to:

* reward meaningful participation (create, buy activity, progress)
* encourage repeat usage and user retention
* provide transparent on-chain leaderboards and ranks (per chain)

## Points (on-chain)

From `BondX.sol`:

### Points scaling (critical)

Points are tracked with **18-decimal precision**, similar to ETH:

* On-chain `userPoints[user]` are stored as **point-wei**
* **1.0 point** = (1 \times 10^{18}) point-wei

### Point constants (per chain family)

**Ethereum / Arbitrum / Base**

* Create token: `POINTS_CREATE_TOKEN = 5`
* Points per 1.0 native token bought: `POINTS_PER_ETH_BUY = 100`
* Graduation bonus: `POINTS_GRADUATION_BONUS = 500`

**BSC**

* Create token: `POINTS_CREATE_TOKEN = 5`
* Points per 1.0 native token bought: `POINTS_PER_ETH_BUY = 30` (BNB)
* Graduation bonus: `POINTS_GRADUATION_BONUS = 500`

### How buy points are computed

On-chain formula (ETH-like variable name, but it is the chain’s native token in wei):

* buy points (point-wei) = `ethAmountWei * POINTS_PER_ETH_BUY`

## How points are earned (high level)

* **Create token**: awards points to the creator
* **Buy activity**: awards points based on native token amount bought (ETH/BNB)
* **Graduation**: awards creator points when the token graduates
* **Sells**: no points (by design)

## Claiming rewards

The contract includes a reward claiming function `claimRewards()` with the intention that **points can be redeemed into BONDX**.

In the current contract design, claiming is enabled once BondXCoin is configured on-chain (`bondXCoinAddress` is set). See `isClaimingEnabled()`.

Because BONDX is an 18-decimal ERC20 and points are tracked with 18-decimal precision, the intended UX of “1 point = 1 BONDX” is achieved by minting the same 18-decimal amount.

## User tiers (points-based)

Tier thresholds are currently derived from **user points**:

* Starter: 0–25
* Bronze: 26–100
* Silver: 101–400
* Gold: 401–1,200
* Platinum: 1,201–5,000
* Diamond: 5,001–25,000
* Legend: 25,001–100,000
* Mythic: 100,001+

Note: tier labels are UI/analytics constructs; on-chain the source of truth is `userPoints[user]` (and per-chain leaderboards/ranks are computed against that).
