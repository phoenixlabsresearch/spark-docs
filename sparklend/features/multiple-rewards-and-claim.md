# Multiple Rewards and Claim

## Multiple Rewards and Claim

Spark Protocol offers the option to have _**multiple rewards**_ per token depending on whether an asset listing to enables an incentive rewards denominated in their protocol tokens.

Spark Protocol also allows a user to claim rewards to another account as well as self and to claim multiple types of rewards per asset in single tx.

The [RewardsController](../contracts/periphery-contracts/rewardscontroller.md) contract is the main contract where the user interacts to claim the rewards of their positions. The users can claim all the rewards or an individual reward per transaction, with a variety of functions that allow more granularity at claim.

## Integration Guide

### Prerequisites

User(s) should already have a position in the protocol. Depending on the market and incentives that are enabled, they should already have a _supply_, _borrow or both_ in one of the incentivised assets.

### Check rewards enabled

To get list of rewards available for the given asset, use the `getRewardsByAsset()` method, passing in the associated _sp/s/vToken_ address of the incentivised asset. Use `getRewardsData()` to get details per reward per asset.

```typescript
const spDaiRewardsList = await rewardsController.getRewardsByAsset(spDaiAddress);

const spDaiRewardOneData = await rewardsController.getRewardsData(
        spDaiAddress,
        rewardOneAddress
    );
```

### Check User(s) reward balance

You can get user reward balance for a given reward token or all reward tokens for a given list of assets using `getUserRewardsBalance()` or `getAllUserRewardsBalance()` respectively.

```typescript
const [, allUnclaimedRewards] = await rewardsController.getAllUserRewardsBalance(
        [spDai.address, aWeth.address],
        userAddress
      );
```

### Claim Rewards

Claim one or all type of rewards _to self_, _another address_ or _onBehalf of an address_ (only authorised claimers) for a given assets list.

#### Self

User can claim one or all type of rewards using `claimRewardsToSelf()` and `claimAllRewardsToSelf()` respectively for the list of assets passed to the method.

{% hint style="info" %}
The `msg.sender` must match the user's address that has accrued the rewards.
{% endhint %}

```tsx

// claims all reward types for asset list [spDai, aWETH, ]
const claimAllRewards = await rewardsController.claimAllRewardsToSelf(
				[spDai.address, aWeth.address, ]
			);
```

#### `onBehalfOf` An Address

Authorised user/contract addresses can claim one or all type of rewards _onBehalfOf,_ the user accruing rewards, using `claimRewardsOnBehalf()` and `claimAllRewardsOnBehalf()` respectively for the list of assets passed to the method.

{% hint style="info" %}
The `msg.sender` must be an authorised claimer set using setClaimer() method, via Governance Vote.
{% endhint %}

```tsx

// claims all reward types for asset list [spDai, aWETH, ]
const claimAllRewardsOnBehalfOf = await rewardsController.claimAllRewardsOnBehalf(
                    [spDai.address],
                    userWithRewards.address,
                    claimer.address
		)
```

#### To Another Address

User can claim one or all type of rewards, to an external account (i.e. an account which may or may not be accruing the rewards being claimed), using `claimRewards()` and `claimAllRewards()` respectively for the list of assets passed to the method.

{% hint style="info" %}
The `msg.sender` must match the user's address that has accrued the rewards
{% endhint %}

```tsx

// claims all reward types for asset list [spDai, aWETH, ] to receivingAccount
const claimAllRewards = await rewardsController.claimAllRewards(
				[spDai.address, aWeth.address, ],
				receivingAccount.address
			);
```
