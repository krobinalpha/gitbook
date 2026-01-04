# 🎁 Rewards & Redemption

BondX uses on-chain points to measure contributions and distribute BONDX rewards.

## The promise: “1 point = 1 BONDX”

If the product promise is “**1 point = 1 BONDX**”, then the redemption mechanism must mint BONDX using 18-decimal units:

* 1 BONDX = \(1 \times 10^{18}\) token units (wei-like units)

This is critical for UX clarity and investor credibility.

## How redemption works (current design)

The BondX contract includes:

* `userPoints[user]` for accumulated points
* `claimRewards(pointsToClaim)` to redeem points into BONDX

Key properties:

* **Claiming is enabled only in Phase 2** (`isPhase2Active`), per chain.
* Points are deducted when claimed, and a mint is performed from the BONDX contract.
* BONDX enforces a **hard max supply**, so redemption is bounded by supply.

## Sustainability and emission control

Even with a hard max supply, investor-grade tokenomics require clarity on:

* expected points emission rates (per phase)
* expected claim rates and redemption behavior
* whether the system introduces any throttles (e.g., per-block, per-day, per-user caps)

If no throttles exist, the effective throttle becomes BONDX max supply and user behavior (which can still create large supply pressure).

## Anti-abuse design notes (current on-chain behavior)

BondX includes several mechanisms that reduce obvious “farm loops”:

* **No points on sells** (reduces self-trading reward loops)
* **Tier bonuses are one-time** per tier per user
* **Progress points** are awarded only on progress increases (delta-based)

## Transparency requirement

If BondX markets “1 point = 1 BONDX”, the deployed contract implementation must match this.

To avoid ambiguity, the correct minting behavior for an 18-decimal ERC20 is:

* claim \(N\) points → mint \(N \times 10^{18}\) BONDX token units

If a deployment uses a different conversion, the UI and documentation should reflect the **actual** conversion rate rather than the intended one.


