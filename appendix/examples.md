# Examples (Fees, Points, Rewards)

These examples are simplified to help investors and users reason about the mechanics.

## Example A — Fees on a 1 ETH buy

Fees are graduation-progress tiered. The total is 1.0% (100 bps), but the split changes.

### Tier 1 example (progress < 35%)

- Creator (0.30%): 0.003 ETH
- Treasury (0.50%): 0.005 ETH
- Buyback (0.20%): 0.002 ETH
- **Total fees**: 0.010 ETH
- **Net ETH applied to reserves**: 0.990 ETH

### Tier 2 example (35% ≤ progress < 70%)

- Creator (0.40%): 0.004 ETH
- Treasury (0.40%): 0.004 ETH
- Buyback (0.20%): 0.002 ETH
- **Total fees**: 0.010 ETH
- **Net ETH applied to reserves**: 0.990 ETH

### Tier 3 / Default example (progress ≥ 70%)

- Creator (0.60%): 0.006 ETH
- Treasury (0.20%): 0.002 ETH
- Buyback (0.20%): 0.002 ETH
- **Total fees**: 0.010 ETH
- **Net ETH applied to reserves**: 0.990 ETH

## Example B — Points on a 1 ETH buy

From `BondX.sol`:

- Ethereum / Arbitrum / Base: `POINTS_PER_ETH_BUY = 100` (so **100 points per 1 ETH**)
- BSC: `POINTS_PER_ETH_BUY = 30` (so **30 points per 1 BNB**)

So a 1 ETH buy yields:

- **100 points** (on ETH-like chains)

## Example C — “1 point = 1 BONDX”

BONDX is an 18-decimal ERC20 and points are tracked with 18-decimal precision. If the user claims 100 points, the UX is:

- user receives **100 BONDX**
- in token units, that is **100 × 10^18**

In the current contract, `claimRewards()` mints the user’s claimable points in the same 18-decimal units, matching this UX.

## Example D — Buyback LP bootstrap (conceptual)

BondX accumulates buyback fees in `accumulatedBuybackFee`. When:

- `buybackLpAdded == false`, and
- `accumulatedBuybackFee` reaches the chain’s `BUYBACK_LP_THRESHOLD`

the contract attempts a one-time BondXCoin/native-token liquidity add on the configured UniswapV2-style router using exactly `BUYBACK_LP_THRESHOLD` (plus a fixed amount of BondXCoin). On success:

- `buybackLpAdded` becomes `true`
- `bondXCoinListed` becomes `true`


