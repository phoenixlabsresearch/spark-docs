# Spark Protocol Overview

The Spark Protocol is decentralised non-custodial liquidity protocol where users can participate as suppliers, borrowers or liquidators. Suppliers provide liquidity to a market and can earn interest on the crypto assets provided, while borrowers are able to borrow in an overcollateralized fashion. Borrowers can also engage in one-block borrow transactions (”flash loans”), which do not require overcollateralization.

## Capital Efficiency

We allow users to optimise their assets supplied to the Spark Protocol in terms of yield generation and borrowing power.

### [Efficiency Mode (eMode)](features/efficiency-mode-emode.md)

The High Efficiency Mode or _**eMode**_ allows borrowers to extract the highest borrowing power out of their collateral when supplied and borrowed assets are correlated in price, particularly when both are derivatives of the same underlying asset (eg. stablecoins pegged to USD).

This can enabling a wave of new use cases such as High leverage forex trading, Highly efficient yield farming (for example, deposit ETH staking derivatives to borrow ETH), Diversified risk management etc.

{% hint style="info" %}
Check out [eMode](features/efficiency-mode-emode.md) for more technical details.
{% endhint %}

### [Isolation Mode](features/isolation-mode.md)

New assets can be listed as _**isolated**_. Borrowers supplying an isolated asset as collateral cannot supply other assets as collateral (though they can still supply to capture yield). Borrowers using an isolated collateral can only borrow stablecoins that have been permitted by the Maker Governance to be borrowable in isolation mode, up to a specified debt ceiling.

![](<.gitbook/assets/image (5).png>)

### [Siloed Borrowing](features/siloed-borrowing.md)

Siloed borrowing allows assets with potentially manipulatable oracles to be listed on Spark as single borrow asset i.e. if a user borrows siloed asset, they cannot borrow any other asset. This helps mitigating the risk associated with such assets from impacting the overall solvency of the protocol. Please see the [Siloed Borrowing](features/siloed-borrowing.md) page for more details.

## Risk Management

Spark Protocol brings a greatly improved set risk parameters and new features to protect the protocol from insolvency.

### [Supply and Borrow Caps](features/supply-borrow-caps.md)

The Maker governance can now configure Borrow and Supply Caps.

* **Borrow Caps:** allow to modulate how much of each asset can be borrowed, which reduces insolvency risk.
* **Supply Caps**: allow to limit how much of a certain asset is supplied to the Spark protocol. This helps reducing exposure to a certain asset and mitigate attacks like infinite minting or price oracle manipulation.

### Granular Borrowing Power Control

In Spark Protocol, it will be possible to lower the borrowing power of any asset to as low as 0% without any impact on existing borrowers (it’s still possible to use the old approach - liquidating existing users - if deemed necessary)

### Risk Admins

Spark Protocol introduces the ability for the Maker Governance to grant entities permission to update the risk parameters with going through governance vote for every change. These entities can be DAOs or automated agents (eg. RiskDAO, Gauntlet) that can build on top of this feature to react automatically in case of unanticipated events.

{% hint style="info" %}
Maker Governance will have the ability to revoke access to existing Risk Admins or add new Risk Admins.
{% endhint %}

### Price Oracle Sentinel

The Sentinel feature introduces a grace period for liquidations and disables borrowing under specific circumstances.

This feature has been specifically designed for L2s to handle eventual downtime of the sequencer (but can be extended to handle other cases, even on L1s, in the future).

### Variable Liquidation Close Factor

The liquidation mechanism has been improved to allow the position to be fully liquidated when it approaches insolvency i.e. _HF < 0.95_ (previously only half of the position could be liquidated at any point).

## Decentralisation

Spark Protocol introduces a new system role - `ASSET_LISTING_ADMIN_ROLE` - that can be granted by the Maker Governance to allow admins to create and set custom asset listing strategies for each asset listing.

## Multiple Rewards Tokens

Spark Protocol offers the option to have _**multiple rewards**_ per token. Now, it is possible for an asset listing to enable additional incentives denominated in native protocol tokens. It is also possible for user to claim multiple reward types per asset in single transaction. Read more in [Multiple Rewards section](features/multiple-rewards-and-claim.md).

## Spark Interface

The Spark interface is hosted on [IPFS](https://ipfs.tech/) in a decentralized manner. Spark maps the following DNS names to the Cloudflare IPFS gateway:
* [https://app.sparkprotocol.io](https://app.sparkprotocol.io) will always point to the latest main IPFS hash with disabled test networks
* [https://staging.sparkprotocol.io](https://staging.sparkprotocol.io) will always point to the latest main IPFS hash with all networks enabled

### IPFS Troubleshooting

If the Cloudflare gateway is not working and you are unable to connect to [app.sparkprotocol.io](https://app.sparkprotocol.io), you can use any public or private IPFS gateway supporting origin isolation to access the Spark interface:
* Go to ```<your favorite public ipfs gateway>/ipns/app.sparkprotocol.io```
* Make sure the gateway supports origin isolation to avoid possible security issues
* You should be redirected to a URL that looks like ```https://app-sparkprotocol-io.<your gateway>```

### Previous Links

The following links have worked previously:
* https://app-sparkprotocol-io.ipns.cf-ipfs.com/#/
* https://app-sparkprotocol-io.ipns.dweb.link/#/
