# Asset / Debt Management

All supply and borrow actions are done via [LendingPool](https://www.notion.so/LendingPool-990bd1490c2a4a038c139c974835332b).

<aside>
💡 Always get latest LendingPool from the [AddressProvider](https://www.notion.so/LendingPoolAddressesProvider-9e318ec7364f4e63a2b7afa8103736de)

</aside>

# Supply into LendingPool

<aside>
💡 On deposit, `LendingPool` pulls funds from the `msg.sender` and transfers `aTokens` to `onBehalf` address.

</aside>

## ERC20

- aave-js SDK
    
    
    ```jsx
    import { TxBuilderV2, Network } from "@aave/protocol-js";
    
    const txBuilder = new TxBuilderV2(Network.kovan, ethprovider_url);
    
    const lendingPool = txBuilder.getLendingPool(Market.Proto);
    
    const Txns = lendingPool.deposit({
       user, // string,
       reserve, // string,
       amount, // string,
    	 onBehalfOf, // ? string
    	 referralCode // ? string
    });
    
    // use web3 wallet to send tx
    for (let i = 0; i < TxObject.length; i++) {
        wallet.sendTransaction(await TxObject[i].tx())
    }
    ```
    
- web3/ethers
    
    ```jsx
    import { Contract, utils } from "ethers"
    const LENDING_POOL_ADDRESS = await addressesProvider.getLendingPool();
    const weth = new Contract(WETH_ADDRESS, WethAbi, signer);
    const lendingPool = new Contract(LENDING_POOL_ADDRESS, LendingPoolAbi, signer);
    
    // Approve LendingPool to spend user's funds
    await weth.approve(LENDING_POOL, constants.MaxUint256);
    
    // On successful deposit onBehalf address receives the aToken
    await lendingPool.deposit(WETH, utils.parseEther(amount), onBehalf, 0);
    ```
    
- solidity
    
    ```objectivec
    ILendingPool lendingPool = ILendingPool(provider.getLendingPool());
    
    // Transfer funds from the caller to the depositing contract
    IERC20(asset).transferFrom(msg.sender, address(this), amount);
    
    // Approve LendingPool to spend your contracts funds
    if (IERC20(asset).allowance(address(this), address(LendingPool)) == 0) {
      erc20.approve(address(LendingPool), uint256(-1));
    }
    
    // Deposit on onBehalf of msg.sender
    lendingPool.deposit(_asset, _amount, msg.sender, 0);
    ```
    

## Native ETH / MATIC

Only `ERC20` tokens can be deposited into the LendingPool. If you want to use your native ETH (or MATIC in case of polygon), you can use wethGateway contract to easily wrap.

- web3/ethers
    
    ```jsx
    import { Contract, utils } from "ethers"
    
    const gateway = new Contract(GATEWAY_ADDRESS, gatewayAbi, signer);
    const LENDING_POOL_ADDRESS = await addressesProvider.getLendingPool();
    
    // After deposit onBehalf address receives the aToken
    await gateway.depositETH(
    	LENDING_POOL_ADDRESS,
    	onBehalf,
    	0,
    	{value: utils.parseEther(amount)}
    );
    ```
    

- solidity
    
    ```objectivec
    // After deposit msg.sender receives the aToken
    IWETHGateway(gatewayAddress).depositETH{ value: msg.value }(
    	provider.getLendingPool(),
    	msg.sender,
    	0
    );
    ```
    

# Borrow from LendingPool

<aside>
💡 `onBehalfOf` must have enough collateral via `deposit()` or have delegated credit to `msg.sender` via `approveDelegation()`. See the [Credit Delegation guide](https://www.notion.so/Credit-Delegation-8c3adacce35a4426ba77d0f1b84eb99b) for more details.

</aside>

## ERC20

- web3/ethers
    
    ```jsx
    const interestRateMode = 1; // 1 = stable, 2 = variable
    
    // Borrow WETH
    await lendingPool.borrow(
    	WETH,
    	amount,
    	interestRateMode,
    	0,
    	onBehalf
    );
    ```
    

- solidity
    
    ```objectivec
    LENDING_POOL = ILendingPool(provider.getLendingPool());
    
    unit256 interestRateMode = 2;  // 1 = stable, 2 = variable
    
    // Borrow onbehalf of msg.sender if address(this) has credit delegated
    ILendingPool(LENDING_POOL).borrow(_asset, _amount, interestRateMode, 0, msg.sender);
    
    // If address(this) holds aTokens i.e. have collateral
    ILendingPool(LENDING_POOL).borrow(_asset, _amount, interestRateMode, 0, address(this));
    ```
    

## Native ETH / MATIC

Only `ERC20` tokens can be borrowed from the LendingPool. If you want to borrow native ETH (or MATIC in case of polygon), you can use wethGateway contract to easily unwarp.

- web3/ethers
    
    ```jsx
    import { Contract, utils } from "ethers"
    
    const gateway = new Contract(GATEWAY_ADDRESS, gatewayAbi, signer);
    const debtTokenContract = new Contract(IDebtTokenABI, DebtTokenAddress);
    
    // Delegate credit to weth gateway
    await debtTokenContract.approveDelegation(GATEWAY_ADDRESS, amount);
    
    // Borrow ETH/MATIC
    await gateway.borrowETH(
    	LENDING_POOL,
    	amount,
    	interestRateMode,
    	0,
    );
    ```
    
- solidity
    
    ```objectivec
    // Always get latest LendingPool from the [AddressProvider](https://www.notion.so/LendingPoolAddressesProvider-9e318ec7364f4e63a2b7afa8103736de)
    LENDING_POOL = ILendingPool(provider.getLendingPool());
    
    unit256 interestRateMode = 2;  // 1 = stable, 2 = variable
    
    // calling contract should have enough credit limit
    IDebtToken(DebtTokenAddress).approveDelegation(gatewayAddress, amount);
    
    // Borrowed amount will be send to the calling contract
    IWETHGateway(gatewayAddress).borrowETH(
    	LENDING_POOL,
    	amount,
    	interestRateMode,
    	0
    );
    ```
    

# Withdraw from LendingPool

<aside>
💡 Only the account holding the `aTokens` can withdraw underlying `asset` from the `LendingPool`

</aside>

## ERC20

- aave-js SDK
- web3/ethers
    
    ```jsx
    import { Contract, utils } from "ethers"
    const LENDING_POOL_ADDRESS = await addressesProvider.getLendingPool();
    const weth = new Contract(WETH_ADDRESS, WethAbi, signer);
    const lendingPool = new Contract(LENDING_POOL_ADDRESS, LendingPoolAbi, signer);
    
    // On successful withdraw onBehalf address receives the underlying asset
    await lendingPool.withdraw(WETH, utils.parseEther(amount), onBehalf);
    ```
    
- solidity
    
    ```objectivec
    ILendingPool lendingPool = ILendingPool(provider.getLendingPool());
    
    // Transfer aTokens from the caller to the withdrawing contract
    IERC20(asset).transferFrom(msg.sender, address(this), amount);
    
    // Withdraw on onBehalf of msg.sender
    lendingPool.withdraw(_asset, _amount, msg.sender);
    ```
    

## Native ETH / MATIC

Only `ERC20` tokens can be withdrawn from the LendingPool. If you want to receive native ETH (or MATIC in case of polygon), you can use wethGateway contract to easily unwrap.

- javascript
    
    ```jsx
    import { Contract, utils } from "ethers"
    
    const gateway = new Contract(GATEWAY_ADDRESS, gatewayAbi, signer);
    const LENDING_POOL_ADDRESS = await addressesProvider.getLendingPool();
    const aWeth = new Contract(aTokenAddress, aTokenAbi, signer);
    
    // Approve WETHGateway to burn user's aTokens
    await aWeth.approve(GATEWAY_ADDRESS, constants.MaxUint256);
    
    // After withdraw to address receives the ETH (or MATIC)
    await gateway.withdrawETH(
    	LENDING_POOL_ADDRESS,
    	amount,
    	to,
    );
    ```
    

- solidity
    
    ```objectivec
    // Always get latest LendingPool from the AddressProvider
    LENDING_POOL = ILendingPool(provider.getLendingPool());
    
    // calling contract should have enough credit limit
    IAToken(ATokenAddress).approve(gatewayAddress, amount);
    
    // Withdrawn amount will be send to `to` address
    IWETHGateway(gatewayAddress).withdrawETH(
    	LENDING_POOL,
    	amount,
    	to
    );
    ```