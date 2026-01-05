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

After Phase 2 is activated (per chain), protocol mechanics change:

* fees are lower overall
* buyback and LP mechanics become active
* rewards claiming is enabled (in the current on-chain design)
