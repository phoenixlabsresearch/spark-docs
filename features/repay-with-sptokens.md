# Repay With spTokens

Allows user to repay with _spTokens_ in case the underlying borrowed asset is locked in the Spark Protocol liquidity pool.

_Example:_ **User have stable DAI debt and also holds spDAI token**

The user in this case can use aDAI to repay DAI debt in single transaction without any approvals or having to withdraw their supplied liquidity to the pool using `repayWithSpTokens` feature.

```tsx
import { Contract, utils } from "ethers";
const poolAbi = require("./abis/pool.json");
const pool = new Contract(POOL_ADDRESS, poolAbi, signer);

// repay amount of DAI debt using spDAI tokens
pool.repayWithSpTokens(DAI.address, amount, 2);

// User must hold spDAI >= amount being repaid
```
