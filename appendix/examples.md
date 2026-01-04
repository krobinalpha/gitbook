# Examples (Fees, Points, Rewards)

These examples are simplified to help investors and users reason about the mechanics.

## Example A — Fees on a 1 ETH buy

### Phase 1
Fee schedule:

- Treasury: 0.5%
- LP: 2.5%
- Buyback: 0%

On 1.0 ETH:

- Treasury fee: 0.005 ETH
- LP fee: 0.025 ETH
- Buyback fee: 0.000 ETH
- Total fees: 0.030 ETH
- Net ETH applied to reserves: 0.970 ETH

### Phase 2
Fee schedule:

- Treasury: 0.3%
- LP: 0.5%
- Buyback: 0.7%

On 1.0 ETH:

- Treasury fee: 0.003 ETH
- LP fee: 0.005 ETH
- Buyback fee: 0.007 ETH
- Total fees: 0.015 ETH
- Net ETH applied to reserves: 0.985 ETH

## Example B — Points on a 1 ETH buy

From `BondX.sol`:

- Phase 1: 10 points per 1 ETH buy
- Phase 2: 4 points per 1 ETH buy

So a 1 ETH buy yields:

- **Phase 1**: 10 points
- **Phase 2**: 4 points

## Example C — “1 point = 1 BONDX”

BONDX is an 18-decimal ERC20. If the user claims 100 points, the intended UX is:

- user receives **100 BONDX**
- in token units, that is **100 × 10^18**

This requires the on-chain minting to use the correct token unit scale.


