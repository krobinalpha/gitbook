# ☸️ Phases & LP Listing

BondX defines two phases:

* **Phase 1**: initial phase, focused on accumulation and growth mechanics.
* **Phase 2**: activated after BondXCoin LP listing conditions are met.

## LP listing threshold

From `BondX.sol`:

* **LP listing threshold**: 10 ETH
* **BondXCoin token amount for LP**: 2,500,000 tokens

## How Phase 2 activates (current on-chain design)

Phase 2 is activated on a chain when BondXCoin is listed on Uniswap on that chain. In the contract:

* Phase 1 LP fees accumulate into `accumulatedLPFee`.
* When `accumulatedLPFee >= LP_LISTING_THRESHOLD`, the owner can trigger listing via `listBondXCoinManually()`.
* Listing sets `bondXCoinListed = true` and `isPhase2Active = true`.

## “Automatic” listing (recommended upgrade)

If BondX wants Phase 2 activation to be **automatic**, the contract can be wired so that once the threshold is reached, a keeper/automation job triggers listing.

Important: this is an **operational choice**:

* **Manual activation** is simpler and reduces automation risk, but requires an admin action.
* **Automated activation** improves UX and consistency, but introduces keeper dependency and requires careful safeguards.

## What happens at listing

When listing occurs:

* LP is created using the configured amounts
* Phase 2 becomes active
* fee schedule switches to Phase 2

## Why phases matter

Phases change:

* fee rates
* whether certain actions happen immediately (e.g., buyback/liquidity add) vs accumulate for later
* points emission rates (Phase 2 reduces points constants)

## User-facing interpretation

* **Phase 1**: higher fees but higher rewards/points emissions (distribution phase).
* **Phase 2**: lower fees and ongoing sustainability mechanics (buyback + LP operations).
