# Token Lifecycle

## Create
A creator calls the contract to create a new token. The token is registered and associated with the creator.

## Trade (early market formation)
Users buy and sell. Each trade:

- updates token reserve state
- updates user trading volume
- may award points (buys award points; sells do not)
- applies fees based on Phase 1 or Phase 2

## Graduation / progress
BondX tracks graduation progress for tokens and can award creators progress-based points as the token advances.

## Phase mechanics
Phase changes affect fee routing and operational behavior (LP / buyback logic). See the Economics section for details.


