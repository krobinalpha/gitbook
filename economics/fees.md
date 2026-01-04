# ◽ Fees

All fee rates below are taken from on-chain constants in `BondX.sol`.

## Fee denominator

Basis points (BPS) use a denominator of 10,000.

## Phase 1 fees (initial)

* **Buyback fee**: 0 bps (0%)
* **Treasury fee**: 50 bps (0.5%)
* **LP fee**: 250 bps (2.5%)

## Phase 2 fees (after LP listing)

* **Buyback fee**: 70 bps (0.7%)
* **Treasury fee**: 30 bps (0.3%)
* **LP fee**: 50 bps (0.5%)

## Where fees go (high level)

* **Treasury fee** is sent to the treasury address and also tracked via an on-chain accumulator.
* **LP fee** is accumulated (Phase 1), then used for LP operations (Phase 2 behavior).
* **Buyback fee** is accumulated or executed depending on phase rules.

See “Treasury, LP & Buyback Flows” for operational detail.
