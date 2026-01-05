# 💸 Economics

BondX economics are defined primarily on-chain and operate independently per chain.

This section explains:

* fee model (market-cap fee tiers)
* BondXCoin LP bootstrap and buyback mechanics
* points and user tiers (volume thresholds and bonuses)
* how treasury and buyback flows work

## User summary

BondX has **no Phase 1 / Phase 2** in the current deployed contract. Instead:

* **Fees are tiered by market cap** (creator + treasury + buyback; no LP fee).
* **Buyback fee** funds:
  * a one-time **BondXCoin LP bootstrap** on Uniswap once a threshold is reached, and then
  * ongoing **buyback + burn** operations when enough buyback ETH accumulates.
* **Claiming rewards** is enabled once BondXCoin is configured on-chain (`bondXCoinAddress` is set).
