# 🪙 BONDX Token

BONDX is the native token used for BondX rewards and incentive distribution.

## Supply

From `BondXCoin.sol`:

* **Max supply**: 1,000,000,000 BONDX
* **Decimals**: 18 (standard ERC20)

BONDX starts with **zero supply** and is minted as rewards, subject to the max supply cap.

## Minting permissions

BONDX can only be minted by the configured BondX contract address:

* `BondXCoin.setBondXContract(address)` can be called by the BONDX owner and can only be set once.
* `BondXCoin.mint(to, amount)` is restricted to `msg.sender == bondXContract` and enforces `totalSupply + amount <= MAX_SUPPLY`.

## Intended utility (current on-chain scope)

Today, BONDX utility is primarily tied to:

* **reward redemption** from earned points (see Rewards & Redemption)
* **ecosystem mechanics** such as buyback + burn and liquidity operations (which affect BONDX market dynamics on that chain)

Additional utilities (e.g., fee discounts, governance, launch perks) should be documented explicitly if/when introduced.


