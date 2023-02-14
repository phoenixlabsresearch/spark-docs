# LendingPoolAddressesProvider

Addresses register of the protocol for a particular market. This contract is immutable and the address will never change. Also see [Deployed Contracts](notion://www.notion.so/developers/deployed-contracts/deployed-contracts) section.

Whenever the `LendingPool` contract is needed, we recommended you fetch the correct address from the `LendingPoolAddressesProvider` smart contract.

The source code can be [found on Github here](https://github.com/aave/protocol-v2/blob/ice/mainnet-deployment-03-12-2020/contracts/protocol/configuration/LendingPoolAddressesProvider.sol).

# Methods

## getMarketId**()**

**`function getMarketId()`**

[Return values](https://www.notion.so/7440bf7055f14a3384ed39b17ed42539)

## getLendingPool**()**

**`function getLendingPool()`**

[Return values](https://www.notion.so/c43cb3b19c424e69ad786fb97ff2401c)

## getLendingPoolConfigurator**()**

**`function getLendingPoolConfigurator()`**

The `LendingPoolConfigurator` is used for configuration methods for each market, e.g.initialising a reserve or updating aTokens.

[Return values](https://www.notion.so/cde9f4be2394477980c91fa6baf3ed7b)

## getLendingPoolCollateralManager**()**

**`function getLendingPoolCollateralManager()`**

The `LendingPoolCollateralManager` is used for management of collateral in the protocol, the main one being for liquidations. The contract should never be called directly, only via the `LendingPool`.

[Return values](https://www.notion.so/0864d774684f4daa86a41f2c6ea981b6)

## getPoolAdmin**()**

**`function getPoolAdmin()`**

[Return values](https://www.notion.so/213ac8f1dc364271b53f5d764a309440)

## getPoolEmergencyAdmin**()**

**`function getPoolEmergencyAdmin()`**

[Return values](https://www.notion.so/937ed36d439d43bba2815c5a4ff250d4)

## getPriceOracle**()**

**`function getPriceOracle()`**

[Return values](https://www.notion.so/4193355a46464b519202b2d050401372)

## getLendingRateOracle**()**

**`function getLendingRateOracle()`**

[Return values](https://www.notion.so/aa9bc8daaf794ea5b50fc8884bc31988)

## getAddress**()**

**`function getAddress(bytes32 id)`**

For example, the [Protocol Data Provider](https://www.notion.so/f86216cfc52b4efdbb7ab7ec1ef53e8e) uses the id: `0x1`

[Return values](https://www.notion.so/7801602f0f0f436ea98708817e05e673)