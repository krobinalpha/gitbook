# 💸 Economics

BondX economics are defined primarily on-chain and operate independently per chain.

This section explains:

* fee model (graduation-progress fee tiers)
* BondXCoin LP bootstrap and buyback mechanics
* points and user tiers (points thresholds)
* how treasury and buyback flows work

## User summary

BondX has **no Phase 1 / Phase 2** in the current deployed contract. Instead:

* **Fees are tiered by graduation progress** (creator + treasury + buyback; no LP fee).
* **Buyback fee** funds:
  * a one-time **BondXCoin LP bootstrap** on the configured UniswapV2-style router once a threshold is reached, and then
  * ongoing **buyback + burn** operations when enough buyback native token accumulates.
* **Claiming rewards** is enabled once BondXCoin is configured on-chain (`bondXCoinAddress` is set).
