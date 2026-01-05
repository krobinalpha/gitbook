# Examples (Fees, Points, Rewards)

These examples are simplified to help investors and users reason about the mechanics.

## Example A — Fees on a 1 ETH buy

Fees are market-cap tiered. The total is 1.0% (100 bps), but the split changes.

### Tier 1 example (market cap < 6 ETH)

- Creator (0.30%): 0.003 ETH
- Treasury (0.50%): 0.005 ETH
- Buyback (0.20%): 0.002 ETH
- **Total fees**: 0.010 ETH
- **Net ETH applied to reserves**: 0.990 ETH

### Tier 2 example (6 ETH ≤ market cap < 10 ETH)

- Creator (0.40%): 0.004 ETH
- Treasury (0.40%): 0.004 ETH
- Buyback (0.20%): 0.002 ETH
- **Total fees**: 0.010 ETH
- **Net ETH applied to reserves**: 0.990 ETH

### Tier 3 / Default example (market cap ≥ 10 ETH)

- Creator (0.60%): 0.006 ETH
- Treasury (0.20%): 0.002 ETH
- Buyback (0.20%): 0.002 ETH
- **Total fees**: 0.010 ETH
- **Net ETH applied to reserves**: 0.990 ETH

## Example B — Points on a 1 ETH buy

From `BondX.sol`:

- 10 points per 1 ETH buy

So a 1 ETH buy yields:

- **10 points**

## Example C — “1 point = 1 BONDX”

BONDX is an 18-decimal ERC20. If the user claims 100 points, the intended UX is:

- user receives **100 BONDX**
- in token units, that is **100 × 10^18**

This requires the on-chain minting to use the correct token unit scale.

## Example D — Buyback LP bootstrap (conceptual)

BondX accumulates buyback fees in `accumulatedBuybackFee`. When:

- `accumulatedBuybackFee >= 5 ETH` and `buybackLpAdded == false`

the contract attempts a one-time BondXCoin/ETH liquidity add on Uniswap using exactly **5 ETH** (plus a fixed amount of BondXCoin). On success:

- `buybackLpAdded` becomes `true`
- `bondXCoinListed` becomes `true`


