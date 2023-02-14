# LendingPool
TODO - update with new contract
The source code can be found on [Github here](https://github.com/aave/protocol-v2/blob/ice/mainnet-deployment-03-12-2020/contracts/protocol/lendingpool/LendingPool.sol)**.**

# Example code

For example code interacting with LendingPool methods, checkout integration guides 👇🏻

[Asset / Debt Management](asset_debt_management.md)

[Flash Loan](flash_loan.md)

[Liquidations](liquidations.md)

# Contract API reference

## Write Methods

### **deposit()**

**`function deposit(address asset, uint256 amount, address onBehalfOf, uint16 referralCode)`**

Deposits `amount` of an `asset` into the protocol, minting the same `amount` of corresponding aTokens, and transferring them to the `onBehalfOf` address.

The `referralCode` is emitted in deposit event and can be for third party referral integrations.

<aside>
💡 When depositing, the `LendingPool` contract must have**`allowance()`**to spend funds on behalf of**`msg.sender`** for at-least**`amount`** for the **`asset`** being deposited. This can be done via the standard ERC20 `approve()` method.

</aside>

[call params](https://www.notion.so/7487dd260d0b4afe93d94beb9d41f9b9)

### **withdraw()**

**`function withdraw(address asset, uint256 amount, address to)`**

Withdraws `amount` of the underlying `asset`, i.e. redeems the underlying token and burns the aTokens.

<aside>
💡 When withdrawing `to`another address,**`msg.sender`**should have`aToken` that will be burned by lendingPool .

</aside>

| Parameter Name | Type | Description |
| --- | --- | --- |
| asset | address | address of the notion://www.notion.so/developers/deployed-contracts/deployed-contracts#supported-assets, not the aToken |
| amount | uint256 | amount deposited, expressed in wei units. Use type(uint).max to withdraw the entire balance. |
| to | address | address that will receive the asset |

### borrow**()**

**`function borrow(address asset, uint256 amount, uint256 interestRateMode, uint16 referralCode, address onBehalfOf)`**

Borrows `amount` of `asset` with `interestRateMode`, sending the `amount` to `msg.sender`, with the debt being incurred by `onBehalfOf`.

<aside>
💡 Note: `onBehalfOf` must have enough collateral via `[deposit()](notion://www.notion.so/developers/the-core-protocol/lendingpool#deposit)` or have delegated credit to `msg.sender` via `[approveDelegation()](notion://www.notion.so/developers/the-core-protocol/debt-tokens#approvedelegation)`. See the [Credit Delegation guide](https://www.notion.so/Credit-Delegation-8c3adacce35a4426ba77d0f1b84eb99b) for more details.

</aside>

| Parameter Name | Type | Description |
| --- | --- | --- |
| asset | address | address of the notion://www.notion.so/developers/deployed-contracts/deployed-contracts#supported-assets |
| amount | uint256 | amount to be borrowed, expressed in wei units |
| interestRateMode | uint256 | the type of borrow debt.
Stable: 1, Variable: 2 |
| referralCode | uint16 | referral code for our referral program. Use 0 for no referral code. |
| onBehalfOf | address | address of user who will incur the debt.
Use msg.sender when not calling on behalf of a different user. |

### repay**()**

**`function repay(address asset, uint256 amount, uint256 rateMode, address onBehalfOf)`**

Repays `onBehalfOf`'s debt `amount` of `asset` which has a `rateMode`.

| Parameter Name | Type | Description |
| --- | --- | --- |
| asset | address | address of the notion://www.notion.so/developers/deployed-contracts/deployed-contracts#supported-assets |
| amount | uint256 | amount to be borrowed, expressed in wei units.
Use uint(-1) to repay the entire debt,  ONLY when the repayment is not executed on behalf of a 3rd party. 
In case of repayments on behalf of another user, it's recommended to send an _amount slightly higher than the current borrowed amount. |
| rateMode | uint256 | the type of borrow debt.
Stable: 1, Variable: 2 |
| onBehalfOf | address | address of user who will incur the debt.
Use msg.sender when not calling on behalf of a different user. |

### swapBorrowRateMode**()**

**`function swapBorrowRateMode(address asset, uint256 rateMode)`**

Swaps the `msg.sender`'s borrow rate modes between stable and variable.

| Parameter Name | Type | Description |
| --- | --- | --- |
| asset | address | address of the notion://www.notion.so/developers/deployed-contracts/deployed-contracts#supported-assets |
| rateMode | uint256 | the rate mode the user is swapping from.
Stable: 1, Variable: 2 |

### setUserUseReserveAsCollateral**()**

**`function setUserUseReserveAsCollateral(address asset, bool useAsCollateral)`**

Sets the `asset` of `msg.sender` to be used as collateral or not.

| Parameter Name | Type | Description |
| --- | --- | --- |
| asset | address | address of the notion://www.notion.so/developers/deployed-contracts/deployed-contracts#supported-assets |
| useAsCollateral | bool | true if the asset should be used as collateral |

### liquidationCall**()**

**`function liquidationCall(address collateral, address debt, address user, uint256 debtToCover, bool receiveAToken)`**

Liquidate positions with a **health factor** below 1. Also see our [Liquidations guide](notion://www.notion.so/developers/guides/liquidations).

When the health factor of a position is below 1, liquidators repay part or all of the outstanding borrowed amount on behalf of the borrower, while **receiving a discounted amount of collateral** in return (also known as a liquidation 'bonus"). Liquidators can decide if they want to receive an equivalent amount of collateral aTokens, or the underlying asset directly. When the liquidation is completed successfully, the health factor of the position is increased, bringing the health factor above 1.

Liquidators can only close a certain amount of collateral defined by a close factor. Currently the **close factor is 0.5**. In other words, liquidators can only liquidate a maximum of 50% of the amount pending to be repaid in a position. The liquidation discount applies to this amount.

Liquidators must `approve()` the `LendingPool` contract to use `debtToCover` of the underlying ERC20 of the`asset` used for the liquidation.

**NOTES**

- *In most scenarios*, profitable liquidators will choose to liquidate as much as they can (50% of the `user` position).
- `debtToCover` parameter can be set to `uint(-1)` and the protocol will proceed with the highest possible liquidation allowed by the close factor.
- To check a user's health factor, use `[getUserAccountData()](notion://www.notion.so/developers/the-core-protocol/lendingpool#getuseracountdata)`.

| Parameter Name | Type | Description |
| --- | --- | --- |
| collateral | address | address of the collateral reserve |
| debt | address | address of the debt reserve |
| user | address | address of the borrower |
| debtToCover | uint256 | amount of asset debt that the liquidator will repay |
| receiveAToken | bool | if true, the user receives the aTokens equivalent of the purchased collateral. If false, the user receives the underlying asset directly. |

### **flashLoan()**

**`function flashLoan(address receiverAddress, address[] calldata assets, uint256[] calldata amounts, uint256[] modes, address onBehalfOf, bytes calldata params, uint16 referralCode)`**

Sends the requested `amounts` of `assets` to the `receiverAddress` contract, passing the included `params`.

If the flash loaned `amounts` + fee is not returned by the end of the transaction, then the transaction will either:

- revert if the associated `mode` is 0,
- `onBehalfOf` incurs a stable debt if `mode` is 1, or
- `onBehalfOf` incurs a variable debt if `mode` is 2.

Your contract which receives the flash loaned amounts **must** conform to the `IFlashLoanReceiver` interface. For more, see the [flash loan guides](notion://www.notion.so/developers/guides/flash-loans).

| Parameter Name | Type | Description |
| --- | --- | --- |
| receiverAddress | address | address of the contract receiving the funds.
Must implement the IFlashLoanReceiver interface. |
| assets | address[] | addresses of the reserves to flashloan |
| amounts | uint256[] | amounts of assets to flashloan.
This needs to contain the same number of elements as assets. |
| modes | uint256[] | the types of debt to open if the flashloan is not returned.
0: Don't open any debt, just revert
1: stable mode debt
2: variable mode debt |
| onBehalfOf | address | if the associated mode is not0 then the incurred debt will be applied to the onBehalfOfaddress.
Note: onBehalfOf must already have notion://www.notion.so/developers/the-core-protocol/debt-tokens#approvedelegation sufficient borrow allowance of the associated asset to msg.sender |
| params | bytes | bytes-encoded parameters to be used by the receiverAddress contract |
| referralCode | uint16 | referral code for our referral program |

## View Methods

### getReserveData**()**

**`function getReserveData(address asset)`**

Returns the state and configuration of the reserve

| Parameter Name | Type | Description |
| --- | --- | --- |
| asset | address | address of the reserve |

| Name | Type | Description |
| --- | --- | --- |
| configuration | uint256 | See the https://github.com/aave/protocol-v2/blob/master/aave-v2-whitepaper.pdf for details on why a bitmask was used. To find out more about these values, see https://docs.aave.com/risk/asset-risk/risk-parameters#risk-parameters-analysis.
bit 0-15: LTV
bit 16-31: Liq. threshold
bit 32-47: Liq. bonus
bit 48-55: Decimals
bit 56: reserve is active
bit 57: reserve is frozen
bit 58: borrowing is enabled
bit 59: stable rate borrowing enabled
bit 60-63: reserved
bit 64-79: reserve factor |
| liquidityIndex | uint128 | liquidity index in ray |
| variableBorrowIndex | uint128 | variable borrow index in ray |
| currentLiquidityRate | uint128 | current supply / liquidity / deposit rate in ray |
| currentVariableBorrowRate | uint128 | current variable borrow rate in ray |
| currentStableBorrowRate | uint128 | current stable borrow rate in ray |
| lastUpdateTimestamp | uint40 | timestamp of when reserve data was last updated |
| aTokenAddress | address | address of associated aToken (tokenised deposit) |
| stableDebtTokenAddress | address | address of associated stable debt token |
| variableDebtTokenAddress | address | address of associated variable debt token |
| interestRateStrategyAddress | address | address of interest rate strategy. See https://docs.aave.com/risk/liquidity-risk/borrow-interest-rate for more info. |
| id | uint8 | the position in the list of active reserves |

### getUserAccountData**()**

**`function getUserAccountData(address user)`**

Returns the user account data across all the reserves

| Parameter Name | Type | Description |
| --- | --- | --- |
| user | address | address of the user |

| Parameter Name | Type | Description |
| --- | --- | --- |
| totalCollateralETH | uint256 | total collateral in ETH of the user |
| totalDebtETH | uint256 | total debt in ETH of the user |
| availableBorrowsETH | uint256 | borrowing power left of the user |
| currentLiquidationThreshold | uint256 | liquidation threshold of the user |
| ltv | uint256 | Loan To Value of the user |
| healthFactor | uint256 | current health factor of the user.
Also see notion://www.notion.so/developers/the-core-protocol/lendingpool#liquidationcall |

### getConfiguration**()**

**`function getConfiguration(address asset)`**

Returns the configuration of the reserve

[call params](https://www.notion.so/5a20ef019e2e40d2969b81e017701d75)

[Return values](https://www.notion.so/f4aea43d950a4cb0b103978c88a6671d)

### getUserConfiguration**()**

**`function getUserConfiguration(address user)`**

Returns the configuration of the user across all the reserves.

| Parameter Name | Type | Description |
| --- | --- | --- |
| user | address | address of the user |

| Return Type | Description |
| --- | --- |
| uint256 | See the https://github.com/aave/protocol-v2/blob/master/aave-v2-whitepaper.pdf for details on why a bitmask was used.
The bitmask is divided into pairs of bits, one pair for each asset. 

The first bit of the pair indicates if it is being used as collateral by the user, the second bit indicates if it is being borrowed. The corresponding assets are in the same position as notion://www.notion.so/developers/the-core-protocol/lendingpool#getreserveslist For example, if the hex value returned is 0x40020, which represents a decimal value of 262176, then in binary it is 1000000000000100000. If we format the binary value into pairs, starting from the right, we get 1 00 00 00 00 00 00 10 00 00.
If we start from the right and move left in the above binary pairs, the third pair is 10. The third reserve listed in notion://www.notion.so/developers/the-core-protocol/lendingpool#getreserveslist is WETH. Therefore the 1 indicates that WETH is used as collateral, and 0 indicates that WETH has not been borrowed by this user. 
If we continue to go to the end of the binary pairs (furthest left), we have 1 which can also be represented as 01. This is the 10th pair, which in notion://www.notion.so/developers/the-core-protocol/lendingpool#getreserveslist is DAI. Therefore the 0 indicates that DAI is not used as collateral, and the 1 indicates that it is being borrowed by this user.
In short, if a user is using WETH as collateral and has borrowed DAI, then the value returned would be 0x40020(in hex) or 262176 (in decimal). |

### getReserveNormalizedIncome**()**

**`function getReserveNormalizedIncome(address asset)`**

Returns the normalized income per unit of `asset`.

A return value of 1e271e27 indicates no income. As time passes, the income is accrued. A value of 2∗1e272∗1e27indicates that for each unit of asset, two units of income have been accrued.

| Parameter Name | Type | Description |
| --- | --- | --- |
| asset | address | address of the reserve |

### getReserveNormalizedVariableDebt**()**

**`function getReserveNormalizedVariableDebt(address asset)`**

Returns the normalized variable debt per unit of `asset`.

A return value of 1e271e27 indicates no debt. As time passes, the debt is accrued. A value of 2∗1e272∗1e27 indicates that for each unit of asset, two units of debt have been accrued.

[call params](https://www.notion.so/619716022b0f433abbb8d3f613faf635)

### paused**()**

**`function paused()`**

Returns `true` if the LendingPool is paused.

### getReservesList**()**

**`function getReservesList()`**

Returns the list of initialized reserves.

### getAddressesProvider**()**

**function getAddressesProvider()**

Returns the addresses provider.

## Error Codes

In order to reduce gas usage and code size, aave contracts return numbered errors. If you are making calls to the protocol and receive numbered errors, you can use our [error code reference guide](notion://www.notion.so/developers/guides/troubleshooting-errors#reference-guide) to know what the error number means. Alternatively, you can also find what the numbers represent by checking the `[Errors.sol](https://github.com/aave/protocol-v2/blob/master/contracts/protocol/libraries/helpers/Errors.sol)`