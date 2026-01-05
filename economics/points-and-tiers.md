# 🔤 Points & User Tiers

BondX includes an on-chain points system and a volume-based tier structure.

Points and tiers are designed to:

- reward meaningful participation (create, buy activity, progress)
- encourage repeat usage and user retention
- provide transparent on-chain leaderboards and ranks (per chain)

## Points (on-chain)

From `BondX.sol`:

Points constants are single-valued in the current deployed contract:

- Create token: `POINTS_CREATE_TOKEN = 5`
- Points per 1 ETH bought: `POINTS_PER_ETH_BUY = 10`
- Graduation bonus: `POINTS_GRADUATION_BONUS = 1000`
- Graduation progress multiplier: `POINTS_GRADUATION_PROGRESS_MULTIPLIER = 1`

## How points are earned (high level)

- **Create token**: awards points to the creator
- **Buy activity**: awards points based on ETH amount bought
- **Graduation / progress**: awards creator points when progress increases
- **Sells**: no points (by design)

## Claiming rewards

The contract includes a reward claiming function `claimRewards(pointsToClaim)` with the intention that **points can be redeemed into BONDX**.

In the current contract design, claiming is enabled once BondXCoin is configured on-chain (`bondXCoinAddress` is set). See `isClaimingEnabled()`.

Because BONDX is an 18-decimal ERC20, teams should ensure the deployed reward minting matches the intended UX (see Tokenomics → Rewards & Redemption).

## Volume tiers (thresholds)

Tier thresholds are based on a user’s total trading volume (ETH units on that chain):

* Bronze: 10 ETH
* Silver: 50 ETH
* Gold: 100 ETH
* Platinum: 500 ETH
* Diamond: 1,000 ETH
* Legend: 5,000 ETH
* Mythic: 10,000 ETH

Note: many UIs also show a “Starter” tier for users below Bronze.

## Tier bonus points

The contract awards one-time bonus points when a tier threshold is reached:

- Bronze: 20
- Silver: 120
- Gold: 300
- Platinum: 2,000
- Diamond: 5,500
- Legend: 36,000
- Mythic: 100,000
