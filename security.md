# Security

## Design considerations

- On-chain accounting for key metrics (fees, volume, points) reduces reliance on centralized reporting.
- Phase-based constraints reduce operational complexity early and enable more advanced operations later.

## Key trust assumptions

- **Admin key risk**: owner permissions exist and must be secured (multisig recommended).
- **DEX assumptions**: Phase 2 mechanics rely on Uniswap-style swaps/liquidity adds, subject to slippage and market conditions.
- **RPC/indexer assumptions**: UIs and dashboards may rely on RPC providers and/or indexing services for speed, even if the source of truth is on-chain.

## Operational best practices

- Use multi-instance-safe indexing (unique constraints on tx hashes + chain id).
- Ensure idempotent event handling and defensive retries.
- Keep chain-specific deployments independent to avoid cross-chain accounting errors.

## Audits
Security audits are recommended prior to major upgrades or large-scale deployment expansion.


