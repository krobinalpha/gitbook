# ☸️ Phases & LP Listing

BondX defines two phases:

* **Phase 1**: initial phase, focused on accumulation and growth mechanics.
* **Phase 2**: activated after BondXCoin LP listing conditions are met.

## LP listing threshold

From `BondX.sol`:

* **LP listing threshold**: 10 ETH
* **BondXCoin token amount for LP**: 2,500,000 tokens

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
