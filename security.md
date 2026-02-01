# 🔐 Security

## Design considerations

* On-chain accounting for key metrics (fees, volume, points) reduces reliance on centralized reporting.
* Fee logic is deterministic and tiered (graduation-progress based), reducing hidden off-chain rules.
* Buyback/LP operations rely on external DEX execution and can fail; failures should be reported transparently.

## Key trust assumptions

* **Admin key risk**: owner permissions exist and must be secured (multisig recommended).
* **DEX assumptions**: buyback and LP bootstrap rely on UniswapV2-style swaps/liquidity adds (e.g., Uniswap/PancakeSwap routers), subject to slippage and market conditions.
* **RPC/indexer assumptions**: UIs and dashboards may rely on RPC providers and/or indexing services for speed, even if the source of truth is on-chain.

## Application-layer security (off-chain)

* **JWT auth**: API access is gated by JWT; sensitive endpoints should require auth + rate limits.

## Operational best practices

* Use multi-instance-safe indexing (unique constraints on tx hashes + chain id).
* Ensure idempotent event handling and defensive retries.
* Keep chain-specific deployments independent to avoid cross-chain accounting errors.

## Audits

Security audits are recommended prior to major upgrades or large-scale deployment expansion.
