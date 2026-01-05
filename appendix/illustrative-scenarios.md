# Illustrative Scenarios

These scenarios are **illustrative**, not forecasts. They exist to make mechanics easier to understand.

## Assumptions (explicit)

* Numbers are shown for a **single selected chain**.
* ETH amounts ignore gas costs.
* Market outcomes are not guaranteed; execution can be affected by slippage and market conditions.
* If “1 point = 1 BONDX” is used, it assumes BONDX is minted at **18-decimal scale** (see Tokenomics → Rewards & Redemption).

## Scenario 1 — Fee tier impact on a 1 ETH buy

BondX fees are tiered by market cap. Total fees are 1.0%, but the split changes:

### Tier 1 (market cap < 6 ETH)

* Creator fee (0.3%): 0.003 ETH
* Treasury fee (0.5%): 0.005 ETH
* Buyback fee (0.2%): 0.002 ETH
* **Total fees**: 0.010 ETH
* **Net into reserves**: 0.990 ETH

### Tier 3 / Default (market cap ≥ 10 ETH)

* Creator fee (0.6%): 0.006 ETH
* Treasury fee (0.2%): 0.002 ETH
* Buyback fee (0.2%): 0.002 ETH
* **Total fees**: 0.010 ETH
* **Net into reserves**: 0.990 ETH

## Scenario 2 — Points earned on a 1 ETH buy

From `BondX.sol`: 10 points per 1 ETH buy.

So a 1 ETH buy yields **10 points**.

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

* a one-time BondXCoin/ETH LP bootstrap (funded by buyback fees), then
* buyback + burn (potential buy pressure + supply reduction).

This can improve market quality and reduce volatility, but it does not guarantee price appreciation.


