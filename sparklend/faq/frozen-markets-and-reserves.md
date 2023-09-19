# Frozen Markets and Reserves

### How is a reserve or market frozen?

A reserve on the Spark Protocol can be frozen by calling the [`setReserveFreeze`](https://github.com/aave/aave-v3-core/blob/ce90d8dabb10679fdd7f6875730d92bca1a6ad99/contracts/protocol/pool/PoolConfigurator.sol#L204) function on the PoolConfigurator contract, which is deployed for each Spark market. This function is callable by addresses with the `RiskAdmin` or `PoolAdmin` role, which is owned by Maker Governance (or Guardian multisig on networks without governance bridge), and can also be granted this role.

### What is a frozen reserve?

A reserve is frozen by calling one which does not allow any new supply, borrow, or rate swap (variable/stable). Repay, withdraw, liquidations, and interest accrual (stable rate rebalances).

### Can a reserve or market be unfrozen?

Yes, the same process and smart contract function can be used to unfreeze as well if conditions are suitable for reserves to be reinstated for supply and borrow.

## Spark Market Reserve Configurations

The table below shows which functions are callable depending on the state of the reserve.

For example, when a reserve is not frozen or paused, if the reserve is `active`, it is still possible to `supply()` assets.

| Function                  | Active | Frozen | Paused | Borrowing Enabled | Stable Borrowing Enabled |
| ------------------------- | ------ | ------ | ------ | ----------------- | ------------------------ |
| Supply                    | Yes    | No     | No     |                   |                          |
| Withdraw                  | Yes    |        | No     |                   |                          |
| Borrow                    | Yes    | No     | No     | Yes               | Depends on the mode      |
| Repay                     | Yes    |        | No     |                   |                          |
| SwapRateMode              | Yes    | No     | No     |                   | Depends on the mode      |
| RebalanceStableBorrowRate | Yes    |        | No     |                   |                          |
| SetUseReserveAsCollateral | Yes    |        | No     |                   |                          |
| Flashloan                 | Yes    |        | No     |                   |                          |
| Liquidate                 | Yes    |        | No     |                   |                          |
| spToken Transfer          |        |        | No     |                   |                          |

The role `emergencyAdmin` can pause a specific reserve.
