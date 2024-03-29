# Siloed Borrowing

This feature allow assets with potentially manipulatable oracles (for example illiquid Uni V3 pairs) to be listed on Spark Protocol as single borrow asset i.e. if user borrows siloed asset, they cannot borrow any other asset. This helps mitigating the risk associated with such assets from impacting the overall solvency of the protocol.

{% hint style="info" %}
[Risk or Pool admin](../contracts/core-contracts/aclmanager.md#roles), selected by Maker Governance, can call [`setSiloedBorrowing`](../contracts/core-contracts/poolconfigurator.md#setsiloedborrowing) to set an asset in _Siloed Borrowing_ mode.
{% endhint %}

## Supply Siloed Assets

A user can supply \_Siloed Asset\_ just like any other asset using [`supply()`](../contracts/core-contracts/pool.md#supply) method in `pool.sol`, though, the asset will not be enabled to use as collateral i.e. supplied amount will not add to total collateral balance of the user.

### Borrow Siloed Assets

{% hint style="danger" %}
User borrowing a _siloed asset_ will \_ **not**\_ be allowed to \_\_ borrow \_\_ any other asset\_.\_
{% endhint %}

User can borrow _Siloed Assets_ using [`borrow()`](../contracts/core-contracts/pool.md#borrow) method in `pool.sol` , only if:

* It is first borrow onBehalf of the address

OR

* Existing user debt is of the same _siloed asset._

To check if user is in Siloed Borrowing state, you can see if underlying asset borrowed by user is s\_iloed\_ using [`getSiloedBorrowing()`](../../core-contracts/sparkprotocoldataprovider.md#getsiloedborrowing) method on SparkProtocolDataProvider.sol.

### Check if Reserved for Siloed Borrowing

```solidity
import {AaveProtocolDataProvider} from '@aave/core-v3/contracts/misc/AaveProtocolDataProvider.sol';
AaveProtocolDataProvider poolDataProvider = AaveProtocolDataProvider(provider.getPoolDataProvider());
// address of the underlying asset
address asset = "0x...";

protocolDataProvider.getSiloedBorrowing(asset);
```

### FAQ

#### How can user enter siloed borrowing state?

User automatically enters siloed borrowing state on their first successful borrow of siloed asset.

#### How does user exit siloed borrowing state?

User must repay all their debt to exist siloed borrowing state.
