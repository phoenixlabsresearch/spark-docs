# Liquidations

## Introduction

A liquidation is a process that occurs when a borrower's health factor goes below 1 due to their collateral value not properly covering their loan/debt value. This might happen when the collateral decreases in value or the borrowed debt increases in value against each other.
In a liquidation, up to 50% of a borrower's debt is repaid and that value + liquidation fee is taken from the collateral available, so after a liquidation that amount liquidated from your debt is repaid.

## How much is the liquidation penalty?

The liquidation penalty (or bonus for liquidators) depends on the asset used as collateral.

## Can you give me an example?

Sure! A couple of them here:

**Example 1**
\
****Bob deposits 10 ETH and borrows 5 ETH worth of DAI.
\
If Bob’s Health Factor drops below 1 his loan will be eligible for liquidation.
\
A liquidator can repay up to 50% of a single borrowed amount = 2.5 ETH worth of DAI.
\
In return, the liquidator can claim a single collateral which is ETH (5% bonus). 
\
The liquidator claims 2.5 + 0.125 ETH for repaying 2.5 ETH worth of DAI.

**Example 2**
\
****Bob deposits 5 ETH and 4 ETH worth of YFI, and borrows 5 ETH worth of DAI
\
If Bob’s Health Factor drops below 1 his loan will be eligible for liquidation.
\
A liquidator can repay up to 50% of a single borrowed amount = 2.5 ETH worth of DAI.
\
In return, the liquidator can claim a single collateral, as the liquidation bonus is higher for YFI (15%) than ETH (5%) the liquidator chooses to claim YFI. 
\
The liquidator claims 2.5 + 0.375 ETH worth of YFI for repaying 2.5 ETH worth of DAI.

## How can I avoid getting liquidated?

To avoid liquidation you can raise your health factor by depositing more collateral assets or repaying part of your loan. By default, repayments increase your health factor more than deposits. Also, it's important to monitor your health factor and keep it high to avoid a liquidation. Keeping your health factor over 2, for example, gives you more of a margin to avoid a liquidation.

You should be mindful of the stablecoin price fluctuations due to market conditions and how it might affect your healthfactor. For example, the market price of USDC 1.00 might not equal exactly USD 1.00, but for example USD 0.95. The price fluctuations of stablecoins, like any assets, affects your healthfactor.

## Can I participate in the liquidations ecosystem?

Yes, liquidations are open to anyone, but there is a lot of competition. Normally liquidators develop their own solutions and bots to be the first ones liquidating loans to get the liquidation bonus.
You can find more details in the [developers liquidation section](https://docs.sparkprotocol.io/developers/guides/liquidations).
