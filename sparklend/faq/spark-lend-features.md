# Spark Lend Features

### Isolation Mode

Isolation mode allows Maker Governance to list new assets as isolated assets, which have a specific debt ceiling. Only certain assets can be borrowed in isolation mode—specifically, approved stablecoins. In order for an asset to become approved for borrowing, assets are voted on by MKR token holders through the Maker Governance. 

The debt ceiling for an isolated asset is represented as the maximum amount in USD that can be borrowed against the user’s collateral with two decimals of precision.

### How can I enter isolation mode?

Entering isolation mode is specific to certain isolated assets that are voted on and approved by Maker Governance. You cannot utilize non-isolated assets as collateral to enter isolation mode. The steps to entering isolation mode are as follows:

1. From the dashboard select an isolated asset to supply.
2. You will then see an information notification explaining that you are entering into isolation mode.
3. Once you have successfully entered isolation mode, you will then be able to supply an isolated asset.
4. You can also borrow assets once in isolation mode; however, you will only be able to borrow stablecoins up to a certain debt ceiling.

### How can I exit isolation mode?

To exit isolation mode, you will need to disable the collateralized isolated asset that you have supplied. 

1. From the “Your Supplies” section, click the slider button to disable the isolated asset. 
2. Confirm the disabled isolation mode setting. You have now successfully exited isolation mode.

### How does isolation mode affect my borrowing power?

Upon entering isolation mode, you will be limited to borrowing stablecoins. This is further evidenced under the “Assets to Borrow” section where you will see the available stablecoins listed.

Each isolated asset will have a specific debt ceiling, which means that it is only possible to borrow up to the specified debt ceiling amount. The debt ceiling is visible on the reserves page of each asset.

### High Efficiency Mode (E-mode)

The E-mode feature maximizes capital efficiency when collateral and borrowed assets have correlated prices. For example, DAI, USDC, USDT are all stablecoins pegged to USD. These stablecoins are all within the same E-mode category. Accordingly, a user supplying DAI in E-mode will have higher collateralization power when borrowing assets like USDC or USDT.

Only assets of the same category (for example stablecoins) can be borrowed in E-mode.

E-mode does not restrict the usage of other assets as collateral. Assets outside of the E-mode category can still be supplied as collateral with normal LTV and liquidation parameters.

### How do I enter E-mode?

To enter E-mode from the dashboard, toggle to the dropdown menu under the “"Your Borrows”" where you will find an “Enable E-mode” button. Initially, the button to enable E-mode will indicate that E-mode is “disabled.” Click “Enable E-mode" ” and follow the instructions in the pop-up. Once you have followed the instructions, you will have enhanced borrowing power (i.e., up to 97% LTV) within E-mode and can only borrow assets within the same category of assets (for example, stablecoins).

### How do I exit E-mode?

To exit E-mode, select “"Disable E-mode”" from the dropdown under the “Your Borrows” section. Follow the instructions in the pop-up to exit E-mode.

### How does E-mode affect my borrowing power?

When E-mode is enabled, you will have higher borrowing power over assets of the same E-mode category.

### How can I use permit?

With Spark Protocol, you can move your assets seamlessly between all Spark Protocol markets over different networks. The permit function of Spark Protocol allows you to move your funds from a wallet by simply signing an approval message instead of approving a transaction on the network to avoid gas fees.