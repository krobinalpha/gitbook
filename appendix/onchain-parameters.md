# On-chain Parameters (BondX.sol)

This table reflects constants/state in the current `BondX.sol`.

## Fees

- `BPS_DENOMINATOR = 10000`

### Fee tier caps (market cap)

- `FEE_TIER1_CAP = 6 ETH`
- `FEE_TIER2_CAP = 10 ETH`
- `FEE_TIER3_CAP = 16 ETH`

### Fee tiers (BPS)

- Tier 1: creator 30, treasury 50, buyback 20
- Tier 2: creator 40, treasury 40, buyback 20
- Tier 3: creator 60, treasury 20, buyback 20
- Default: creator 60, treasury 20, buyback 20

## Treasury & buyback accounting

- `accumulatedTreasuryFee` (ETH)
- `accumulatedBuybackFee` (ETH)
- `buybackLpAdded` (bool)
- `bondXCoinListed` (bool)

## Buyback LP bootstrap

- `BUYBACK_LP_THRESHOLD = 5 ETH`
- `BUYBACK_LP_TOKEN_AMOUNT = 50,000,000 BondXCoin`
- `MIN_BUYBACK_AMOUNT = 0.01 ETH`
- `MIN_LP_ADD_AMOUNT = 0.01 ETH`

## Bonding curve / supply

- `TOTAL_SUPPLY = 1,000,000,000`
- `VIRTUAL_TOKEN_RESERVES = 1,000,000,000`
- `VIRTUAL_ETH_RESERVES = 1 ETH`

## Graduation config

- `marketCapUnit = 0.01 ETH` (owner-settable)
- `DEFAULT_GRADUATION_MULTIPLIER = 3`
- `graduationEth = DEFAULT_GRADUATION_MULTIPLIER * marketCapUnit` (default behavior)

## Points

- `POINTS_CREATE_TOKEN = 5`
- `POINTS_PER_ETH_BUY = 10`
- `POINTS_GRADUATION_BONUS = 1000`
- `POINTS_GRADUATION_PROGRESS_MULTIPLIER = 1`

## Volume tier thresholds (ETH)

- Bronze: 10
- Silver: 50
- Gold: 100
- Platinum: 500
- Diamond: 1,000
- Legend: 5,000
- Mythic: 10,000

## Tier bonus points

- Bronze: 20
- Silver: 120
- Gold: 300
- Platinum: 2,000
- Diamond: 5,500
- Legend: 36,000
- Mythic: 100,000
