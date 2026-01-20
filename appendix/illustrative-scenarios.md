# Illustrative Scenarios

These scenarios are **illustrative**, not forecasts. They exist to make mechanics easier to understand.

## Assumptions (explicit)

* Numbers are shown for a **single selected chain**.
* Native token amounts (ETH/BNB) ignore gas costs.
* Market outcomes are not guaranteed; execution can be affected by slippage and market conditions.
* If “1 point = 1 BONDX” is used, it assumes BONDX is minted at **18-decimal scale** (see Tokenomics → Rewards & Redemption).

## Scenario 1 — Fee tier impact on a 1 ETH buy

BondX fees are tiered by graduation progress. Total fees are 1.0%, but the split changes:

### Tier 1 (progress < 35%)

* Creator fee (0.3%): 0.003 ETH
* Treasury fee (0.5%): 0.005 ETH
* Buyback fee (0.2%): 0.002 ETH
* **Total fees**: 0.010 ETH
* **Net into reserves**: 0.990 ETH

### Tier 3 / Default (progress ≥ 70%)

* Creator fee (0.6%): 0.006 ETH
* Treasury fee (0.2%): 0.002 ETH
* Buyback fee (0.2%): 0.002 ETH
* **Total fees**: 0.010 ETH
* **Net into reserves**: 0.990 ETH

## Scenario 2 — Points earned on a 1 ETH buy

From `BondX.sol`:

- Ethereum / Arbitrum / Base: **100 points per 1 ETH** (`POINTS_PER_ETH_BUY = 100`)
- BSC: **30 points per 1 BNB** (`POINTS_PER_ETH_BUY = 30`)

So a 1 ETH buy yields **100 points** (on ETH-like chains).

## Scenario 3 — “Fees vs rewards” (conceptual)

If points are redeemable for BONDX, the user’s “net benefit” depends on:

* how many points are earned per unit volume,
* whether claiming is enabled (current design: enabled once `bondXCoinAddress` is set),
* the BONDX market price at redemption time,
* and any throttles/caps the system introduces (policy choice).

This is why professional reporting should show both:

* fee totals (on-chain accumulators), and
* rewards issued / claimed (points and BONDX minted), per chain.

## Scenario 4 — Buyback / LP bootstrap intuition (non-guaranteed)

Part of fees can route into:

* a one-time BondXCoin/native-token LP bootstrap (funded by buyback fees), then
* buyback + burn (potential buy pressure + supply reduction).

This can improve market quality and reduce volatility, but it does not guarantee price appreciation.


