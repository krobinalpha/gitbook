# On-chain Parameters (BondX.sol)

This table reflects constants/state in the current `BondX.sol`.

## Fees

* `BPS_DENOMINATOR = 10000`

### Fee tier selection (graduation-progress based)

Fee tiers are selected based on `realEthReserves` as a **percentage of the token’s `graduationEth`** target:

* Tier 1: (0%) → (35%) of `graduationEth`
* Tier 2: (35%) → (70%) of `graduationEth`
* Tier 3: (70%) → (100%) of `graduationEth`
* Default: (\ge 100%) of `graduationEth` (same as Tier 3 in the current contract)

### Fee tiers (BPS)

* Tier 1: creator 30, treasury 50, buyback 20
* Tier 2: creator 40, treasury 40, buyback 20
* Tier 3: creator 60, treasury 20, buyback 20
* Default: creator 60, treasury 20, buyback 20

## Treasury & buyback accounting

* `accumulatedTreasuryFee` (native token: ETH/BNB)
* `accumulatedBuybackFee` (native token: ETH/BNB)
* `buybackLpAdded` (bool)
* `bondXCoinListed` (bool)

## Buyback LP bootstrap

`BUYBACK_LP_THRESHOLD` is chain-specific:

* Ethereum / Arbitrum / Base: `5` (**5 ETH**)
* BSC: `15` (**15 BNB**)
* `BUYBACK_LP_TOKEN_AMOUNT = 50,000,000 BondXCoin`
* `MIN_BUYBACK_AMOUNT = 0.01` (native token: ETH/BNB)
* `MIN_LP_ADD_AMOUNT = 0.01` (native token: ETH/BNB)

## Bonding curve / supply

* `TOTAL_SUPPLY = 1,000,000,000`
* `VIRTUAL_TOKEN_RESERVES = 1,000,000,000`
* `VIRTUAL_ETH_RESERVES` is chain-specific:
  * Ethereum / Arbitrum / Base: `1` (**1 ETH**)
  * BSC: `3` (**3 BNB**)

## Graduation config

`GRADUATION_THRESHOLD` is a constant per chain family:

* Ethereum / Arbitrum / Base: `5` (5 **ETH**)
* BSC: `15` (**15 BNB**)

## Points

Points use 18-decimal precision (“point-wei”):

* **1.0 point** = (1 \times 10^{18}) point-wei

Constants:

* `POINTS_CREATE_TOKEN = 5` (awarded as `5 * 1e18` point-wei)
* `POINTS_GRADUATION_BONUS`:
  * Ethereum / Arbitrum / Base: `500` (awarded as `500 * 1e18` point-wei)
  * BSC: `500` (awarded as `500 * 1e18` point-wei)
* `POINTS_PER_ETH_BUY`:
  * Ethereum / Arbitrum / Base: `100`
  * BSC: `30`

Buy points formula:

* buy points (point-wei) = `ethAmountWei * POINTS_PER_ETH_BUY`

## Rewards claiming (BondXCoin)

* Claiming is enabled when `bondXCoinAddress != address(0)`
* `claimRewards()` mints BondXCoin in the same 18-decimal units as points, enabling the UX of “1 point = 1 BONDX” (when points are displayed as `formatUnits(pointsWei, 18)`).
