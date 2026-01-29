# 🧑‍💻 Trader Flow

This section describes the trader experience and what is measurable on-chain.

## 1) Discover tokens

Traders browse newly created tokens on a specific chain.

Because BondX is multi-chain with per-chain independence, traders should always know:

* which chain they are trading on
* which contract deployment applies to that chain

## 2) Buy / sell

Traders can buy and sell tokens. Each trade:

* updates per-token reserve state
* applies graduation-progress tiered fees (creator + treasury + buyback)
* updates the trader’s on-chain trading volume
* updates total platform trading volume (per chain)

## 3) Earn points and tiers

Points are awarded for buys (and other actions). Tier bonuses are awarded when users cross volume thresholds.

## 4) Claim rewards

In the current on-chain design, rewards claiming is enabled once BondXCoin is configured on-chain (`bondXCoinAddress` is set).
