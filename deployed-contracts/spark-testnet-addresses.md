# Spark Protocol Testnet Addresses

### The Spark Protocol is available on the following testnets:

* Ethereum - Goerli

TODO - update contracts

{% hint style="warning" %}
For assets on testnets, we use different versions of the token (e.g. testnet Dai) which are mintableERC20. This is to ensure enough liquidity for our reserves and to easily mint more tokens when needed.
{% endhint %}

\
💡 Click through the tabs to get addresses of the deployed contracts on various chains.

{% tabs %}
{% tab title="Goerli" %}
```
┌─────────┬──────────────────────────────────┬──────────────────────────────────────────────┬────────────────────────┐
│ (index) │               name               │                   account                    │        balance         │
├─────────┼──────────────────────────────────┼──────────────────────────────────────────────┼────────────────────────┤
│    0    │            'deployer'            │ '0x77c45699A715A64A7a7796d5CEe884cf617D5254' │ '0.600631889717317961' │
│    1    │            'aclAdmin'            │ '0x77c45699A715A64A7a7796d5CEe884cf617D5254' │ '0.600631889717317961' │
│    2    │         'emergencyAdmin'         │ '0x77c45699A715A64A7a7796d5CEe884cf617D5254' │ '0.600631889717317961' │
│    3    │           'poolAdmin'            │ '0x77c45699A715A64A7a7796d5CEe884cf617D5254' │ '0.600631889717317961' │
│    4    │ 'addressesProviderRegistryOwner' │ '0x77c45699A715A64A7a7796d5CEe884cf617D5254' │ '0.600631889717317961' │
│    5    │       'treasuryProxyAdmin'       │ '0x04c94825C3e3539e0f2bB21d435302d08B2Dbd77' │         '0.08'         │
│    6    │      'incentivesProxyAdmin'      │ '0x04c94825C3e3539e0f2bB21d435302d08B2Dbd77' │         '0.08'         │
│    7    │   'incentivesEmissionManager'    │ '0x77c45699A715A64A7a7796d5CEe884cf617D5254' │ '0.600631889717317961' │
│    8    │     'incentivesRewardsVault'     │ '0x77c45699A715A64A7a7796d5CEe884cf617D5254' │ '0.600631889717317961' │
└─────────┴──────────────────────────────────┴──────────────────────────────────────────────┴────────────────────────┘

Deployments
===========
┌─────────────────────────────────────────┬──────────────────────────────────────────────┐
│                 (index)                 │                   address                    │
├─────────────────────────────────────────┼──────────────────────────────────────────────┤
│      PoolAddressesProviderRegistry      │ '0xC87385b5E62099f92d490750Fcd6C901a524BBcA' │
│               SupplyLogic               │ '0xF61Cffd6071a8DB7cD5E8DF1D3A5450D9903cF1c' │
│               BorrowLogic               │ '0xde9Fa4A2d8435d45b767506D4A34791fa0371f79' │
│            LiquidationLogic             │ '0x63E537A69b3f5B03F4f46c5765c82861BD874b6e' │
│               EModeLogic                │ '0x0082ef98229887020962624Cbc66092Da5D82AaC' │
│               BridgeLogic               │ '0x02444D214962eC73ab733bB00Ca98879efAAa73d' │
│            ConfiguratorLogic            │ '0xE341D799E61d9caDBB6b05539f1d10aAdfA24d70' │
│             FlashLoanLogic              │ '0xB7348Df015BB2e67449406FD1283DbAc99Ab716B' │
│                PoolLogic                │ '0x18eE6714Bb1796b8172951D892Fb9f42a961C812' │
│              TreasuryProxy              │ '0xFbAF383eB6c757faCb8cb19B68d5131aEbc5c11e' │
│           Treasury-Controller           │ '0x5665007321915c8f0E72d041315bA1AD15065337' │
│         Treasury-Implementation         │ '0xA5375B08232a0f5e911c8a92B390662e098a579A' │
│               WETHGateway               │ '0xd5B55D3Ed89FDa19124ceB5baB620328287b915d' │
│          WalletBalanceProvider          │ '0x75CC0f0E3764be7594772D08EEBc322970CbB3a9' │
│            ERC20Faucet-Spark            │ '0x1ca525Cd5Cb77DB5Fa9cBbA02A0824e283469DBe' │
│       PoolAddressesProvider-Spark       │ '0xc4dCB5126a3AfEd129BC3668Ea19285A9f56D15D' │
│          PoolDataProvider-Spark         │ '0x9BE876c6DC42215B00d7efe892E2691C3bc35d10' │
│    WETH-TestnetPriceAggregator-Spark    │ '0x60E4B131f0F219c72b0346675283E73888e4AB24' │
│     DAI-TestnetPriceAggregator-Spark    │ '0x2A5Acddb524B9454204Ed54EAB51Faf24250a397' │
│    LINK-TestnetPriceAggregator-Spark    │ '0x5b48AE7B44e1b6000d5E9227Af362223AfA87b1A' │
│    USDC-TestnetPriceAggregator-Spark    │ '0x30Ce0bA21A92E14b889F4f31748650EFA8D4C860' │
│    WBTC-TestnetPriceAggregator-Spark    │ '0x2Cb17b22e3Aff6e291D3448C11f39779A576ae17' │
│    USDT-TestnetPriceAggregator-Spark    │ '0x5838fD84a94B3Bc30EE4BDF10AD981Da3310a6a9' │
│    AAVE-TestnetPriceAggregator-Spark    │ '0x87a3F24060BbbAD5dfCE055f24d253f84B11326d' │
│    EURS-TestnetPriceAggregator-Spark    │ '0xf6dc74ec7851695AD549BbF88d371C0A62E9Be23' │
│           Pool-Implementation           │ '0x88c806c9d3aF1b055e65e68Dc336c0065B6dC807' │
│     PoolConfigurator-Implementation     │ '0xC096019F8d41e474BB0d04D4194479B8c67d943a' │
│           ReservesSetupHelper           │ '0x87A5b1cD19fC93dfeb177CCEc3686a48c53D65Ec' │
│             ACLManager-Spark            │ '0x4c952A81A72A6BA2919a658feff1e7F023e4aadc' │
│             Spark ProtocolOracle-Spark            │ '0x5bed0810073cc9f0DacF73C648202249E87eF6cB' │
│           FallbackOracle-Spark          │ '0x0000000000000000000000000000000000000000' │
│             Pool-Proxy-Spark            │ '0x368EedF3f56ad10b9bC57eed4Dac65B26Bb667f6' │
│       PoolConfigurator-Proxy-Spark      │ '0x723d17Ee6a668C011F01553D19B850E425075665' │
│             IncentivesProxy             │ '0x0C501fB73808e1BD73cBDdd0c99237bbc481Bb58' │
│             EmissionManager             │ '0xefF40A6d9De203A8806F4F62D86d5C4c5856965E' │
│       IncentivesV2-Implementation       │ '0x6904a3C18A37B219A59C9c8C6ABB7B1C35fdd7c4' │
│       PullRewardsTransferStrategy       │ '0xe14fe1e916817111Db9c51ff505189Ffe7bc7Dd2' │
│               SpToken-Spark              │ '0xF2EBFA003f04f38Fc606a37ab8D1c015c015725c' │
│       DelegationAwareSpToken-Spark       │ '0x6EF3DFaC236763AA74509B04C0feF0B2f3F5aD3A' │
│          StableDebtToken-Spark          │ '0x7D17eCD9fc4F64F180227216befb9d8E2c723135' │
│         VariableDebtToken-Spark         │ '0x1342dd8Ff58aee340e3C25268A4d08168cC5d990' │
│  ReserveStrategy-rateStrategyStableTwo  │ '0x8557b3992278299E620ebc111A61C1c542d45261' │
│ ReserveStrategy-rateStrategyVolatileOne │ '0xFd2D746cB7d2194DaB321133E28A7072B0945386' │
│  ReserveStrategy-rateStrategyStableOne  │ '0x6120276aA5B7cF545Ed3Fb82FfE30c9fbB4D8267' │
│            WETH-SpToken-Spark            │ '0x27B4692C93959048833f40702b22FE3578E77759' │
│       WETH-VariableDebtToken-Spark      │ '0x2b848bA14583fA79519Ee71E7038D0d1061cd0F1' │
│        WETH-StableDebtToken-Spark       │ '0xCAF956bD3B3113Db89C0584Ef3B562153faB87D5' │
│             DAI-SpToken-Spark            │ '0x310839bE20Fc6a8A89f33A59C7D5fC651365068f' │
│       DAI-VariableDebtToken-Spark       │ '0xEa5A7CB3BDF6b2A8541bd50aFF270453F1505A72' │
│        DAI-StableDebtToken-Spark        │ '0xbaBd1C3912713d598CA2E6DE3303fC59b19d0B0F' │
│            LINK-SpToken-Spark            │ '0x6A639d29454287B3cBB632Aa9f93bfB89E3fd18f' │
│       LINK-VariableDebtToken-Spark      │ '0x593D1bB0b6052FB6c3423C42FA62275b3D95a943' │
│        LINK-StableDebtToken-Spark       │ '0x4f094AB301C8787F0d06753CA3238bfA9CFB9c91' │
│            USDC-SpToken-Spark            │ '0x1Ee669290939f8a8864497Af3BC83728715265FF' │
│       USDC-VariableDebtToken-Spark      │ '0x3e491EB1A98cD42F9BBa388076Fd7a74B3470CA0' │
│        USDC-StableDebtToken-Spark       │ '0xF04958AeA8b7F24Db19772f84d7c2aC801D9Cf8b' │
│            WBTC-SpToken-Spark            │ '0xc0ac343EA11A8D05AAC3c5186850A659dD40B81B' │
│       WBTC-VariableDebtToken-Spark      │ '0x480B8b39d1465b8049fbf03b8E0a072Ab7C9A422' │
│        WBTC-StableDebtToken-Spark       │ '0x15FF4188463c69FD18Ea39F68A0C9B730E23dE81' │
│            USDT-SpToken-Spark            │ '0x73258E6fb96ecAc8a979826d503B45803a382d68' │
│       USDT-VariableDebtToken-Spark      │ '0x45c3965f6FAbf2fB04e3FE019853813B2B7cC3A3' │
│        USDT-StableDebtToken-Spark       │ '0x7720C270Fa5d8234f0DFfd2523C64FdeB333Fa50' │
│            AAVE-SpToken-Spark            │ '0xC4bf7684e627ee069e9873B70dD0a8a1241bf72c' │
│       AAVE-VariableDebtToken-Spark      │ '0xad958444c255a71C659f7c30e18AFafdE910EB5a' │
│        AAVE-StableDebtToken-Spark       │ '0x4a8aF512B73Fd896C8877cE0Ebed19b0a11B593C' │
│            EURS-SpToken-Spark            │ '0xc31E63CB07209DFD2c7Edb3FB385331be2a17209' │
│       EURS-VariableDebtToken-Spark      │ '0x257b4a23b3026E04790c39fD3Edd7101E5F31192' │
│        EURS-StableDebtToken-Spark       │ '0x512ad2D2fb3Bef82ca0A15d4dE6544246e2D32c7' │
│          MockFlashLoanReceiver          │ '0x1931722c81F8A6b27d21a8Abfc167134D2F1a790' │
│        UiIncentiveDataProvider          │ '0xACFd610B51ac6B70F030B277EA8A2A8D2143dC7A' │
│          UiPoolDataProviderV3           │ '0xC576539371a2f425545B7BF4eb2a14Eee1944a1C' │
└─────────────────────────────────────────┴──────────────────────────────────────────────┘

Mintable Reserves and Rewards
┌────────────────────────────────┬──────────────────────────────────────────────┐
│            (index)             │                   address                    │
├────────────────────────────────┼──────────────────────────────────────────────┤
│ WETH-TestnetMintableERC20-Spark│ '0x2e3A2fb8473316A02b8A297B982498E661E1f6f5' │
│ DAI-TestnetMintableERC20-Spark │ '0xDF1742fE5b0bFc12331D8EAec6b478DfDbD31464' │
│ LINK-TestnetMintableERC20-Spark│ '0x07C725d58437504CA5f814AE406e70E21C5e8e9e' │
│ USDC-TestnetMintableERC20-Spark│ '0xA2025B15a1757311bfD68cb14eaeFCc237AF5b43' │
│ WBTC-TestnetMintableERC20-Spark│ '0x8869DFd060c682675c2A8aE5B21F2cF738A0E3CE' │
│ USDT-TestnetMintableERC20-Spark│ '0xC2C527C0CACF457746Bd31B2a698Fe89de2b6d49' │
│ AAVE-TestnetMintableERC20-Spark│ '0x63242B9Bd3C22f18706d5c4E627B4735973f1f07' │
│ EURS-TestnetMintableERC20-Spark│ '0xaA63E0C86b531E2eDFE9F91F6436dF20C301963D' │
└────────────────────────────────┴──────────────────────────────────────────────┘
```
{% endtab %}
{% endtabs %}
