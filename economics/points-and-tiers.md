# 🔤 Points & User Tiers

BondX includes an on-chain points system and a volume-based tier structure.

## Points (on-chain)

From `BondX.sol`:

### Phase 1 points

* Create token: 5
* Points per 1 ETH bought: 10
* Graduation bonus: 100
* Graduation progress multiplier: 10

### Phase 2 points (reduced)

* Create token: 2
* Points per 1 ETH bought: 4
* Graduation bonus: 40
* Graduation progress multiplier: 4

## Volume tiers (thresholds)

Tier thresholds are based on a user’s total trading volume (ETH units on that chain):

* Bronze: 10 ETH
* Silver: 50 ETH
* Gold: 100 ETH
* Platinum: 500 ETH
* Diamond: 1,000 ETH
* Legend: 5,000 ETH
* Mythic: 10,000 ETH

Note: many UIs also show a “Starter” tier for users below Bronze.

## Tier bonus points

The contract awards one-time bonus points when a tier threshold is reached.

### Phase 1 tier bonus points

* Bronze: 20
* Silver: 120
* Gold: 300
* Platinum: 2,000
* Diamond: 5,500
* Legend: 36,000
* Mythic: 100,000

### Phase 2 tier bonus points

* Bronze: 6
* Silver: 36
* Gold: 90
* Platinum: 600
* Diamond: 1,650
* Legend: 10,800
* Mythic: 30,000
