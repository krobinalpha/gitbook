# Security

## Design considerations

- On-chain accounting for key metrics (fees, volume, points) reduces reliance on centralized reporting.
- Phase-based constraints reduce operational complexity early and enable more advanced operations later.

## Operational best practices

- Use multi-instance-safe indexing (unique constraints on tx hashes + chain id).
- Ensure idempotent event handling and defensive retries.
- Keep chain-specific deployments independent to avoid cross-chain accounting errors.

## Audits
Security audits are recommended prior to major upgrades or large-scale deployment expansion.


