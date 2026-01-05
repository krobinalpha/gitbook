# 🧑‍🎨 Creator Flow

This section describes the creator journey at a product level.

## 1) Create a token

A creator initiates a token creation transaction. The BondX contract deploys a new token contract and registers:

* the token address
* the creator address
* metadata (name, symbol, description, URI)

The contract also maintains a list of tokens created by a creator (for transparent counting and rankings).

## 2) Optional initial buy

Creators may optionally include an initial buy in the creation transaction (if supported by the UI/flow). This:

* seeds initial trading activity
* starts accumulating points and volume metrics immediately

## 3) Grow to graduation

As trading occurs:

* the token’s progress toward its graduation target can be tracked
* creators may earn progress-based points as the token advances

## 4) Post-launch behavior

Post-launch mechanics are always active in the current design, but behavior depends on configuration and thresholds:

* **Fees are market-cap tiered** (creator/treasury/buyback; no LP fee).
* **Buyback mechanics** execute when enough buyback fee accumulates (subject to minimum thresholds and DEX conditions).
* **BondXCoin LP bootstrap** occurs once buyback accumulation reaches the on-chain threshold (sets `buybackLpAdded = true`).
* **Rewards claiming** is enabled once BondXCoin is configured (`bondXCoinAddress` is set).
