# Protocol Features Summary

The Spark Protocol offers features which may only be available in select networks or market. The following guide gives a breakdown of each features availability across all Spark Protocol deployments.

## Page Contents

* [Network Feature Summary](protocol-feature-summary.md#network-feature-summary)
  * [AAVE Staking](protocol-feature-summary.md#staking)
  * [Maker Governance](protocol-feature-summary.md#on-chain-governance)
  * [Snapshot Voting](protocol-feature-summary.md#snapshot-voting)
  * [Cross-Chain Governance Bridges](protocol-feature-summary.md#cross-chain-governance-bridges)
* [Market Feature Summary](protocol-feature-summary.md#market-feature-summary)
  * [Repay With Collateral](protocol-feature-summary.md#repay-with-collateral)
  * [Collateral Swap](protocol-feature-summary.md#collateral-swap)
  * [Repay with spTokens](protocol-feature-summary.md#repay-with-sptokens)

## Network Feature Summary

| Network     | AAVE Staking | Governance Voting | Cross-Chain Governance Execution | Snapshot Voting                           |
| ----------- | ------------ | ----------------- | -------------------------------- | ----------------------------------------- |
| ETH Mainnet | Yes          | Yes               | ---                              | AAVE, aAAVE (V2 Market), stkAAVE, stkABPT |
| Polygon     | No           | No                | Yes                              | AAVE, aAAVE (V2 Market)                   |
| Avalanche   | No           | No                | No                               | AAVE, aAAVE (V2 Market)                   |
| Arbitrum    | No           | No                | No                               | None                                      |
| Optimism    | No           | No                | No                               | None                                      |
| Fantom      | No           | No                | No                               | None                                      |
| Harmony     | No           | No                | No                               | None                                      |

## Market Feature Summary

| Market         | Repay With Collateral | Collateral Swap | Repay With spTokens |
| -------------- | --------------------- | --------------- | ------------------ |
| V2 ETH Mainnet | Yes                   | Yes             | No                 |
| V2 AMM         | No                    | No              | No                 |
| V2 Polygon     | Yes                   | Yes             | No                 |
| V2 Avalanche   | Yes                   | Yes             | No                 |
| V3 Polygon     | Yes                   | Yes             | Yes                |
| V3 Avalanche   | Yes                   | Yes             | Yes                |
| V3 Arbitrum    | No                    | No              | Yes                |
| V3 Optimism    | No                    | No              | Yes                |
| V3 Fantom      | Yes                   | Yes             | Yes                |
| V3 Harmony     | No                    | No              | Yes                |

## Repay With Collateral

The _repay with collateral_ feature allows borrowers to repay their borrowed assets using supplied liquidity within the protocol.

This feature is enabled via [ParaSwapRepayAdapter](https://github.com/spark-protocol/spark-protocol-periphery/blob/master/contracts/adapters/paraswap/ParaSwapRepayAdapter.sol). The user must first approve the contract to pull SpTokens to successfully repay with collateral.

### Supported Markets

Feature available on following **mainnet** markets:

* [V2 Ethereum Main](https://docs.sparkprotocol.io/developers/v/2.0/deployed-contracts/deployed-contracts)
* [V2 Polygon](https://docs.sparkprotocol.io/developers/v/2.0/deployed-contracts/matic-polygon-market)
* [V2 Avalanche](https://docs.sparkprotocol.io/developers/v/2.0/deployed-contracts/avalanche-market)
* [V3 Polygon](../deployed-contracts/v3-mainnet/polygon.md)
* [V3 Avalanche](../deployed-contracts/v3-mainnet/avalanche.md)
* [V3 Fantom](../deployed-contracts/v3-mainnet/fantom.md)

{% hint style="info" %}
This feature does not support repayment of a borrow transaction with the same type of asset (e.g., repaying borrowed USDC with USDC collateral). For repayments with same type of collateral asset see \[Repay With SpTokens feature]\(about:blank#repay-with-sptokens).
{% endhint %}

## Collateral Swap

The _collateral swap_ feature allows the user to swap supplied liquidity in one asset type to another asset type without a separate withdrawal and supply transaction (e.g., swapping _aUSDC_ to _aDAI_ in a single transaction).

The _collateral swap_ feature is enabled via the [ParaSwapLiquiditySwapAdapter](https://github.com/spark-protocol/spark-protocol-periphery/blob/master/contracts/adapters/paraswap/ParaSwapLiquiditySwapAdapter.sol). The user must approve the contract to pull SpTokens in order to successfully swap liquidity.

### Supported Markets

The _collateral swap_ feature is available on following **mainnet** markets:

* [V2 Ethereum Main](https://docs.sparkprotocol.io/developers/v/2.0/deployed-contracts/deployed-contracts)
* [V2 Polygon](https://docs.sparkprotocol.io/developers/v/2.0/deployed-contracts/matic-polygon-market)
* [V2 Avalanche](https://docs.sparkprotocol.io/developers/v/2.0/deployed-contracts/avalanche-market)
* [V3 Polygon](../deployed-contracts/v3-mainnet/polygon.md)
* [V3 Avalanche](../deployed-contracts/v3-mainnet/avalanche.md)
* [V3 Fantom](../deployed-contracts/v3-mainnet/fantom.md)

## Repay With SpTokens

_Repay with SpTokens_ is a new Spark Protocol native feature, which allows the user to repay borrowed assets with supplied liquidity of the same asset type in the pool (e.g., repay borrowed _USDC_ with _aUSDC)_. Additional details can be located at [New Feature: repay with sptoken](../whats-new/repay-with-sptokens.md).

### Supported Markets

The _repay with SpTokens_ feature is available on all V3 **production** and **testnet** markets:

* [V3 Polygon](../deployed-contracts/v3-mainnet/polygon.md)
* [V3 Avalanche](../deployed-contracts/v3-mainnet/avalanche.md)
* [V3 Fantom](../deployed-contracts/v3-mainnet/fantom.md)
* [V3 Harmony](../deployed-contracts/v3-mainnet/harmony.md)
* [V3 Optimism](../deployed-contracts/v3-mainnet/optimism.md)
* [V3 Arbitrum](../deployed-contracts/v3-mainnet/arbitrum.md)

## Staking

{% hint style="info" %}
Existing feature from Maker Governance.
{% endhint %}

An AAVE or ABPT [Spark Protocol Balancer Pool Token](https://pools.balancer.exchange/#/pool/0xc697051d1c6296c24ae3bcef39aca743861d9a81/about) holder can stake their AAVE or ABPT in the Safety Module to enhance protocol solvency and earn Safety Incentives. Upon the occurrence of a shortfall event, up to 30% of the token holder’s stake can be slashed to cover the deficit, providing an additional risk mitigation mechanism for the protocol.

{% hint style="info" %}
The staking option is only available on Ethereum Mainnet. Learn more about staking risks \[here]\(https://docs.sparkprotocol.io/faq/migration-and-staking)
{% endhint %}

## Snapshot Voting

{% hint style="info" %}
Existing feature from Maker Governance.
{% endhint %}

The [Spark Protocol Snapshot Space](https://snapshot.org/#//spark-protocol.eth) is a designated place for voters to gauge the community sentiment for on-chain votes and decide off-chain proposals. Voting on Snapshot proposals is done via a gasless signature and is compatible with a variety of assets and chains. A list of available voting strategies can be viewed [here](protocol-feature-summary.md#network-feature-summary) or queried in realtime via this [GraphQL endpoint](https://hub.snapshot.org/graphql?query=%0Aquery%20Spaces%20%7B%0A%20%20spaces\(%0A%20%20%20%20first%3A%2020%2C%0A%20%20%20%20skip%3A%200%2C%0A%20%20%20%20orderBy%3A%20%22created%22%2C%0A%20%20%20%20orderDirection%3A%20desc%2C%0A%20%20%20%20where%3A%20%7Bid%3A%20%22/spark-protocol.eth%22%7D%0A%20%20\)%20%7B%0A%20%20%20%20id%0A%20%20%20%20name%0A%20%20%20%20about%0A%20%20%20%20network%0A%20%20%20%20symbol%0A%20%20%20%20strategies%20%7B%0A%20%20%20%20%20%20name%0A%20%20%20%20%20%20network%0A%20%20%20%20%20%20params%0A%20%20%20%20%7D%0A%20%20%20%20admins%0A%20%20%20%20members%0A%20%20%20%20filters%20%7B%0A%20%20%20%20%20%20minScore%0A%20%20%20%20%20%20onlyMembers%0A%20%20%20%20%7D%0A%20%20%20%20plugins%0A%20%20%7D%0A%7D).

## On-Chain Governance

{% hint style="info" %}
Existing feature from Maker Governance.
{% endhint %}

[Maker Governance](https://docs.sparkprotocol.io/developers/v/2.0/protocol-governance/governance) allows holders of AAVE or stkAAVE to vote and propose changes and/or upgrades to the protocol and governance. The governance process is described [here](https://docs.sparkprotocol.io/governance/) in more detail.

{% hint style="info" %}
Maker Governance is only enabled on Ethereum mainnet.
{% endhint %}

## Cross-Chain Governance Bridges

{% hint style="info" %}
Relatively new feature integrated on chains that support cross-chain messaging.
{% endhint %}

All voting for Maker Governance proposals occurs on Ethereum mainnet. Governance bridges can be used to take the result of proposal voting on Ethereum mainnet to execute proposals on other chains. [This repo](https://github.com/spark-protocol/governance-crosschain-bridges) contains the technical implementation for cross-chain bridges.

{% hint style="info" %}
The cross-chain bridge is currently available on the Polygon network.
{% endhint %}
