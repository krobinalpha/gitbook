# 🪙 Token Lifecycle

## Create
A creator calls the contract to create a new token. The token is registered and associated with the creator. The system also tracks the creator’s token list for transparent counting and rankings.

## Trade (early market formation)

Users buy and sell. Each trade:

* updates token reserve state
* updates user trading volume
* may award points (buys award points; sells do not)
* applies market-cap tiered fees (creator + treasury + buyback)

## Graduation / progress

BondX tracks graduation progress for tokens and can award creators progress-based points as the token advances.

## Ongoing mechanics

As trading continues, buyback fees can fund:

- a one-time BondXCoin/ETH LP bootstrap, and
- buyback + burn operations (subject to thresholds and DEX execution conditions).
