# Rewards

In Spark Protocol, the rewards system has been updated. Now spToken, variableDebtToken and stableDebtToken has an attached array which can accumulate any number of rewards. Each Spark Protocol market contains a [RewardsController](../../periphery-contracts/rewardscontroller.md) contract which registers the reward emissions for each spToken and debtToken. 

This guide details the steps for registering a new reward on the `RewardsController`.

- [ARC]
- [AIP]
- [Creating Proposal]
- [Add to Spark Protocol Ui]

## ARC

The ARC (Spark Protocol Request for Comment) is the first step in the proposal process. This is where the idea is proposed, and the community can discuss the proposal. All ARCs should follow these standard [requirements](https://docs.sparkprotocol.io/governance/arcs). In addition, new incentive proposals should specify:

- Assets receiving rewards
- Duration of rewards program
- Total emission amount

## AIP

The AIP is a document containing the proposal details which is uploaded to IPFS. The hash of this documented is passed as a parameter when the on-chain proposal is submitted. To create an AIP for a reward emission, follow the steps from the AIP [repo](https:///spark-protocol.github.io/aip/).

Sample AIPs:

- https://github.com/spark-protocol/aip/pull/93

Once the AIP has been reviewed and merged to generate an ipfs hash, and the payload has been created, the proposal can now be submitted on-chain.

## Create Proposal
`EMISSION_ADMIN` set by owner of the EmissionManager contract can configure rewards by calling `configureAssets`.

## Add To Spark Protocol Ui

In order for your reward token name and symbol to appear on the Spark Protocol frontend, you will need to add your asset to the [Spark Protocol Interface repo](https://github.com/spark-protocol/interface/blob/main/CONTRIBUTING.md#token-addition).