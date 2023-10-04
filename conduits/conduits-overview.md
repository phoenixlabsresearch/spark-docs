# Conduits Overview

{% hint style="info" %}
It is recommend to have a working understanding of the following topics:

**Maker Allocation System** \
**subDAOs**
{% endhint %}

Liquidity is one of the main challenges for a protocol. Some only work as intended once they’ve reached a high level of sustained liquidity and most rip the benefits of economies of scale once that is achieved.

Maker has grown DAI to become the largest decentralised stablecoin, behind only to the fiat backed USDC and USDT, stabilising it with different mechanisms that have proven long term viability.

Through the Maker Allocation System, subDAOs provide liquidity directly to protocols. Having Maker as the ultimate Liquidity Provider (LP) allows protocols to benefit from predictable and sustained liquidity at scale.

Conduits provide a standardized way for Maker subDAOs to provide said liquidity to protocols, managing the movement of funds between them. You can think of them as deposit boxes for assets where each entity interacts with it in predefined ways.

While DAI is the main asset used within conduits, any asset can be used within them. The Maker Allocation System includes swapping functionality.

A single conduit gives access to all subDAOs to the same protocol, allowing for competition and specialization from the subDAOs, and optionality for the protocol.



The main benefits of Conduits include,

* Security: common design patterns, limited scoped modules, circuit-breakers
* Flexibility: build on top of existing logic, add custom logic and/or technology
* Safety: Maker Governance has admin power over the entire Maker Allocation System

### **Providing Liquidity as a subDAO**

Under the Maker Endgame model, subDAOs allocate capital to the best yielding investment opportunities, managing risk effectively in the face of competition for the highest return.

All subDAOs have equal access to yield based opportunities, based on an Asset & Liability Management (ALM) framework, subDAOs make the decision to provide liquidity to the target protocols.

The ALM framework defines the logic within the constraints set by [**The Stability and Liquidity Scope Framework (MIP103)**](https://forum.makerdao.com/t/mip103-the-stability-and-liquidity-scope-framework/19675), supported by the the ALM Capitalization Requirements defined in MIP102 regarding collateral asset types based on the conversion delay and slippage tolerance.

**subDAO User Experience with Conduits**

The subDAO can deposit DAI in the conduit by calling `deposit()`

The subDAO can withdraw DAI from the conduit by calling `withdraw()`



### **Integrating Maker liquidity as a Protocol**

Conduits and the Maker Allocation System provide an unprecedented opportunity to acquire best in class liquidity for DeFi protocols.

Protocols need to ensure that the conduits are built and audited, and provide a sound business case for a subDAO to initiate the assessment of the entire protocol.

**Requirements to have Maker subDAOs providing liquidity**

* Introductory post on the subDAO’s forum/main communication channel
* Build & audit conduit contracts
* Financial risk assessment
* Legal risk assessment (if off-chain)

### **Peg stability & pulling liquidity**

Maker’s objective is to sustainable grow and manage DAI to become a major stablecoin. To that end, the ability to quickly (speed) and efficiently (slippage) pull liquidity is critical in order to ensure a stable peg.

subDAOs should be able to unwind positions as quickly as possible with the least impact on price as possible. The ALM requirements limit the exposure to asset types based on this condition.

Therefore, conduits should include logic to ensure the soundness of this mechanism. For example, the Spark Conduit has a RequestFunds() function that will trigger an increase in the borrow rate if the request is bigger than the available funds (non-utilized)

**subDAO User Experience with Conduits**

The protocol can withdraw DAI from the conduit by calling`(DrawFunds()`

The subDAO can request withdrawing DAI from the conduit by calling `RequestFunds()`

The protocol can check if there is a fund request by calling `getFundRequests()`

The protocol can deposit DAI in the conduit by calling `ReturnFunds()`

## Technical Specification

The most important thing for a Conduit is that their interface allows for two main functions, `deposit` and `withdraw`.

[https://github.com/makerdao/dss-allocator](https://github.com/makerdao/dss-allocator)



The main interface:&#x20;

### Reference implementations

| Example                              | Repository                                                                                                                                                   |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Onchain lending protocol (SparkLend) | [https://github.com/marsfoundation/spark-conduits](https://github.com/marsfoundation/spark-conduits)                                                         |
| Off-chain protocol (RWA)             | [https://github.com/makerdao/dss-conduits/blob/master/src/ArrangerConduit.sol](https://github.com/makerdao/dss-conduits/blob/master/src/ArrangerConduit.sol) |

### Introduction (Summary)

Under the Maker Endgame model, subDAOs allocate capital to the best yielding investment opportunities, managing risk effectively in the face of competition for the highest return.

The `**IAllocatorConduit**` acts as a mediator between subDAOs (Allocators) and external protocols (Arrangers), handling the deposit and withdrawal of DAI.

### Glossary

* `Ilk`: Unique identifier that is used to identify an AllocatorDAO.
* `Allocator Vault`: Smart contract that deploys can mint NST/DAI on behalf of an AllocatorDAO and move it as desired.
* `Router`: Smart contract that facilitates the movement of funds between different strategies. Controlled by the `Allocator Vault`.
* `Arranger`: Third-party entity responsible for making use of the deployed capital to generate yield. (e.g. Monetalis, Blocktower)
* `Conduit`: Smart contract that moves funds back and forth from multiple `Router` contracts to a single `Arranger` according to codified and pre-defined rules.
* `subDAO`: entity responsible for allocating capital

![Untitled](../.gitbook/assets/1.png)

### Functions

A set of functions are privileged based on the assigned **`role`** of the user:

* subDAO: entity responsible for allocating capital
* Arranger: entity responsible for the execution of the investment
*   **`deposit`**: This function is used to deposit tokens into the Conduit. It takes parameters **`ilk`** (a unique identifier), **`asset`** (the address of the asset to deposit), and **`amount`** (the amount of tokens to deposit).

    From the Conduit, the funds can be deployed to a yield bearing strategy. This can happen atomically in the case of DeFi protocols, or can happen in a separate function call made by a permissioned actor in the case of Real World Asset strategies.

<figure><img src="../.gitbook/assets/2.png" alt=""><figcaption></figcaption></figure>

* **`withdraw`**: This function is used to withdraw tokens from the Conduit. It takes parameters **`ilk`** (a unique identifier), **`asset`** (the address of the asset to withdraw), and **`maxAmount`** (the maximum amount of tokens to withdraw). This can pull funds atomically from a yield bearing strategy in the case of DeFi protocols, or can pull the funds directly from the Conduit in the case of a Real World Asset strategy where the permissioned actor has returned the funds manually. Both situations require that there is available liquidity, which is why `maxWithdraw` exists.

<figure><img src="../.gitbook/assets/3.png" alt=""><figcaption></figcaption></figure>

* **`maxDeposit`**: This function is a view function, meaning it does not modify the contract state. It is used to get the maximum possible deposit amount for a specific **`asset`** and **`ilk`**.
* **`maxWithdraw`**: This function is also a view function and is used to get the maximum possible withdrawal amount for a specific **`asset`** and **`ilk`**.

### Events

* Deposit (ilk, asset, source, amount)
* Withdraw (ilk, asset, destination, amount)

| variable    | data type | example                       |
| ----------- | --------- | ----------------------------- |
| ilk         | bytes32   | 0x53554244414f2d31 (SUBDAO-1) |
| asset       | address   |                               |
| source      | address   |                               |
| destination | address   |                               |
| amount      | uint256   |                               |
