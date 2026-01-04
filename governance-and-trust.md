# Governance & Trust Assumptions

BondX includes administrative controls. Investors should understand what is controlled by the owner/admin and what is immutable.

## What is controlled today

In the current on-chain design, the owner can typically:

- set key addresses (e.g., treasury, BONDX token address)
- update operational parameters (e.g., router address, pricing constants such as market cap unit)
- manually trigger certain actions (e.g., listing BONDX liquidity / activating Phase 2)
- manually graduate tokens (admin override paths)

This creates a trust assumption: the admin key must be secured and governed responsibly.

## Recommended governance posture (best practice)

- Use a **multisig** for all owner/admin permissions.
- Add a **timelock** for sensitive parameter changes where feasible.
- Publish a clear policy for:
  - emergency actions
  - parameter changes
  - upgrade / migration plans

## Transparency commitments

BondX should commit to:

- publishing the admin addresses (multisig) per chain
- publishing a changelog for parameter updates
- documenting any planned governance decentralization roadmap


