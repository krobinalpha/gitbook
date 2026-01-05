# Illustrative Scenarios

These scenarios are **illustrative**, not forecasts. They exist to make mechanics easier to understand.

## Assumptions (explicit)

* Numbers are shown for a **single selected chain**.
* ETH amounts ignore gas costs.
* Market outcomes are not guaranteed; execution can be affected by slippage and market conditions.
* If “1 point = 1 BONDX” is used, it assumes BONDX is minted at **18-decimal scale** (see Tokenomics → Rewards & Redemption).

## Scenario 1 — Phase 1 vs Phase 2 fee impact on a 1 ETH buy

### Phase 1 (3.0% total)

* Treasury fee (0.5%): 0.005 ETH
* LP fee (2.5%): 0.025 ETH
* Buyback fee (0%): 0.000 ETH
* **Total fees**: 0.030 ETH
* **Net into reserves**: 0.970 ETH

### Phase 2 (1.5% total)

* Treasury fee (0.3%): 0.003 ETH
* LP fee (0.5%): 0.005 ETH
* Buyback fee (0.7%): 0.007 ETH
* **Total fees**: 0.015 ETH
* **Net into reserves**: 0.985 ETH

## Scenario 2 — Points earned on a 1 ETH buy

From `BondX.sol`:

* Phase 1: 10 points per 1 ETH buy
* Phase 2: 4 points per 1 ETH buy

So a 1 ETH buy yields:

* **Phase 1**: 10 points
* **Phase 2**: 4 points

## Scenario 3 — “Recover high fees with high rewards” (conceptual)

In Phase 1, the user pays higher fees but earns more points. If points are redeemable for BONDX, the user’s “net benefit” depends on:

* how many points are earned per unit volume,
* whether claiming is enabled (current design: Phase 2),
* the BONDX market price at redemption time,
* and any throttles/caps the system introduces (policy choice).

This is why professional reporting should show both:

* fee totals (on-chain accumulators), and
* rewards issued / claimed (points and BONDX minted), per chain.

## Scenario 4 — Phase 2 flywheel intuition (non-guaranteed)

In Phase 2, part of fees can route into:

* buyback + burn (potential buy pressure + supply reduction), and
* liquidity adds (deeper liquidity over time).

This can improve market quality and reduce volatility, but it does not guarantee price appreciation.


