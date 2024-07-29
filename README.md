
# Basin audit details
- Total Prize Pool: $37,750 in USDC
  - HM awards: $23,520 in USDC
  - QA awards: $980 in USDC 
  - Judge awards: $4,500 in USDC
  - Validator awards: $2,000 in USDC
  - Scout awards: $750 in USDC
  - Mitigation Review: $6,000 in USDC (*Opportunity goes to top 3 backstage wardens based on placement in this audit who RSVP.*)
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2024-07-basin/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts July 29, 2024 20:00 UTC
- Ends August 8, 2024 20:00 UTC

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2024-07-basin/blob/main/4naly3er-report.md).


_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._

All findings in the following audit reports:

* 06/16/23: [Basin Halborn Report](https://arweave.net/1IKi4iqRvu3qu_GdcLY4f3u9PgvOMvuRltU7AIXAEyA) @ [e5441fc](https://github.com/BeanstalkFarms/Basin/tree/e5441fc78f0fd4b77a898812d0fd22cb43a0af55)
* 06/16/23: [Basin Cyfrin Report](https://arweave.net/usT3ClfjHwpX32OXnh5De1aH79csX1PMoXJCghXBaps) @ [e5441fc](https://github.com/BeanstalkFarms/Basin/tree/e5441fc78f0fd4b77a898812d0fd22cb43a0af55)
* 10/05/23: [Basin Code4rena Report](https://code4rena.com/reports/2023-07-basin) @ [7e51c02](https://github.com/code-423n4/2023-07-basin/tree/7e51c025d32aff3f2456842c83cda66cda274d11)
* All bug reports from the Immunefi program listed [here](https://community.bean.money/bug-reports).


# Overview

# Basin
![basin(green)-512x512 (1)](https://github.com/code-423n4/2024-07-basin/blob/main/basin(green)-512x512%20(1).png?raw=true) ![512x512-MF](https://github.com/code-423n4/2024-07-basin/blob/main/512x512-MF.png?raw=true)

Code Version: `1.0.0` 
Whitepaper Version: `1.0.0`

### Multi Flow

The Multi Flow Pump implementation is also included in this repository at [MultiFlowPump.sol](/src/pumps/MultiFlowPump.sol).

Code Version: `1.0.0` 
Whitepaper Version: `1.0.0`

## About

Basin is a composable EVM-native decentralized exchange protocol.

- [Audits](#audits)
- [Documentation](#documentation)
    - [Motivation](#motivation)
- [License](#license)

## Audits

* [Cyfrin Basin Audit](https://basin.exchange/cyfrin-basin-audit.pdf)
* [Halborn Basin Audit](https://basin.exchange/halborn-basin-audit.pdf)

## Documentation

* [Basin Whitepaper](https://basin.exchange/basin.pdf)
* [Multi Flow Whitepaper](https://basin.exchange/multi-flow-pump.pdf)
* [Basin Docs](https://docs.basin.exchange)

A [{Well}](/src/Well.sol) is a constant function AMM that allows the provisioning of liquidity into a single pooled on-chain liquidity position.

Each Well is defined by its Tokens, Well function, and Pump.
- The **Tokens** define the set of ERC-20 tokens that can be exchanged in the Well.
- The **Well function** defines an invariant relationship between the Well's reserves and the supply of LP tokens. See [{IWellFunction}](/src//interfaces/IWellFunction.sol).
- **Pumps** are an on-chain oracles that are updated upon each interaction with the Well. See [{IPump}](/src/interfaces/IPump.sol).

A Well's tokens, Well function, and Pump are stored as immutable variables during Well construction to prevent unnecessary SLOAD calls during operation.

Wells support swapping, adding liquidity, and removing liquidity in balanced or imbalanced proportions.

Wells maintain two components of state:
- a balance of tokens received through Well operations ("reserves")
- an ERC-20 LP token representing pro-rata ownership of the reserves

Well functions and Pumps can independently choose to be stateful or stateless.

Including a Pump is optional.

Each Well implements ERC-20, ERC-2612 and the [{IWell}](/src/interfaces/IWell.sol) interface.

### Motivation

Allowing composability of the pricing function and oracle at the Well level is a deliberate design decision with significant implications. 

In particular, a standard AMM interface invoking composable components allows for developers to iterate upon the underlying pricing functions and oracles, which greatly impacts gas and capital efficiency. 

However, this architecture shifts much of the attack surface area to the Well's components. Users of Wells should be aware that anyone can deploy a Well with malicious components, and that new Wells SHOULD NOT be trusted without careful review. This understanding is particularly important in the DeFi context in which Well data may be consumed via on-chain registries or off-chain indexing systems.

The Wells architecture aims to outline a simple interface for composable AMMs and leave the process of evaluating a given Well's trustworthiness as the responsibility of the user. To this end, future work may focus on development of on-chain Well registries and factories which create or highlight Wells composed of known components.

An example factory implementation is provided in [{Aquifer}](/src/Aquifer.sol) without any opinion regarding the trustworthiness of Well functions and the Pumps using it. Wells are not required to be deployed via this mechanism.

## License

[MIT](https://github.com/BeanstalkFarms/Basin/blob/master/LICENSE.txt)


## Links

- **Previous audits:**  All can be found [here](https://docs.basin.exchange/resources/audits)
- **Documentation:** https://docs.basin.exchange/
- **Website:** https://basin.exchange
- **X/Twitter:** https://twitter.com/basinexchange
- **Discord:** https://basin.exchange/discord

---

# Scope

*See [scope.txt](https://github.com/code-423n4/2024-07-basin/blob/main/scope.txt)*

### Files in scope


| File   | Logic Contracts | Interfaces | nSLOC | Purpose | Libraries used |
| ------ | --------------- | ---------- | ----- | -----   | ------------ |
| [/src/functions/Stable2.sol](https://github.com/code-423n4/2024-07-basin/blob/main/src/functions/Stable2.sol) | 1| **** | 194 | | src/interfaces/IBeanstalkWellFunction.sol, src/interfaces/ILookupTable.sol, src/functions/ProportionalLPToken2.sol, forge-std/interfaces/IERC20.sol |
| [/src/functions/StableLUT/Stable2LUT1.sol](https://github.com/code-423n4/2024-07-basin/blob/main/src/functions/StableLUT/Stable2LUT1.sol) | 1| **** | 2150 | | src/interfaces/ILookupTable.sol |
| [/src/WellUpgradeable.sol](https://github.com/code-423n4/2024-07-basin/blob/main/src/WellUpgradeable.sol) | 1| **** | 70 | | src/Well.sol, ozu/proxy/utils/UUPSUpgradeable.sol, ozu/access/OwnableUpgradeable.sol, oz/token/ERC20/utils/SafeERC20.sol, src/interfaces/IAquifer.sol |
| **Totals** | **3** | **** | **2414** | | |

### Files out of scope

*See [out_of_scope.txt](https://github.com/code-423n4/2024-07-basin/blob/main/out_of_scope.txt)*

| File         |
| ------------ |
| ./mocks/functions/MockEmptyFunction.sol |
| ./mocks/functions/MockFunctionBad.sol |
| ./mocks/pumps/MockFailPump.sol |
| ./mocks/pumps/MockPump.sol |
| ./mocks/tokens/MockToken.sol |
| ./mocks/tokens/MockTokenFeeOnTransfer.sol |
| ./mocks/tokens/MockTokenNoName.sol |
| ./mocks/tokens/ReentrantMockToken.sol |
| ./mocks/wells/MockInitFailWell.sol |
| ./mocks/wells/MockReserveWell.sol |
| ./mocks/wells/MockStaticWell.sol |
| ./mocks/wells/MockWellUpgradeable.sol |
| ./script/deploy/Aquifer.s.sol |
| ./script/deploy/AquiferWell.s.sol |
| ./script/deploy/MockPump.s.sol |
| ./script/deploy/Well.s.sol |
| ./script/deploy/helpers/Logger.sol |
| ./script/helpers/WellDeployer.sol |
| ./script/simulations/stableswap/StableswapCalcRatiosLiqSim.s.sol |
| ./script/simulations/stableswap/StableswapCalcRatiosSwapSim.s.sol |
| ./src/Aquifer.sol |
| ./src/Well.sol |
| ./src/functions/ConstantProduct.sol |
| ./src/functions/ConstantProduct2.sol |
| ./src/functions/ProportionalLPToken.sol |
| ./src/functions/ProportionalLPToken2.sol |
| ./src/interfaces/IAquifer.sol |
| ./src/interfaces/IBeanstalkWellFunction.sol |
| ./src/interfaces/ILookupTable.sol |
| ./src/interfaces/IMultiFlowPumpWellFunction.sol |
| ./src/interfaces/IWell.sol |
| ./src/interfaces/IWellErrors.sol |
| ./src/interfaces/IWellFunction.sol |
| ./src/interfaces/pumps/ICumulativePump.sol |
| ./src/interfaces/pumps/IInstantaneousPump.sol |
| ./src/interfaces/pumps/IMultiFlowPumpErrors.sol |
| ./src/interfaces/pumps/IPump.sol |
| ./src/libraries/ABDKMathQuad.sol |
| ./src/libraries/LibBytes.sol |
| ./src/libraries/LibBytes16.sol |
| ./src/libraries/LibClone.sol |
| ./src/libraries/LibContractInfo.sol |
| ./src/libraries/LibLastReserveBytes.sol |
| ./src/libraries/LibMath.sol |
| ./src/libraries/LibWellConstructor.sol |
| ./src/libraries/LibWellUpgradeableConstructor.sol |
| ./src/pumps/MultiFlowPump.sol |
| ./src/utils/Clone.sol |
| ./src/utils/ClonePlus.sol |
| ./test/Aquifer.t.sol |
| ./test/LiquidityHelper.sol |
| ./test/Stable2/LookupTable.t.sol |
| ./test/Stable2/Well.Stable2.AddLiquidity.t.sol |
| ./test/Stable2/Well.Stable2.Bore.t.sol |
| ./test/Stable2/Well.Stable2.RemoveLiquidity.t.sol |
| ./test/Stable2/Well.Stable2.RemoveLiquidityImbalanced.t.sol |
| ./test/Stable2/Well.Stable2.RemoveLiquidityOneToken.t.sol |
| ./test/Stable2/Well.Stable2.Shift.t.sol |
| ./test/Stable2/Well.Stable2.Skim.t.sol |
| ./test/Stable2/Well.Stable2.SwapFrom.t.sol |
| ./test/Stable2/Well.Stable2.SwapTo.t.sol |
| ./test/SwapHelper.sol |
| ./test/TestHelper.sol |
| ./test/Well.AddLiquidity.t.sol |
| ./test/Well.AddLiquidityFeeOnTransfer.Fee.t.sol |
| ./test/Well.AddLiquidityFeeOnTransfer.NoFee.t.sol |
| ./test/Well.Bore.t.sol |
| ./test/Well.DuplicateTokens.t.sol |
| ./test/Well.FeeOnTransfer.t.sol |
| ./test/Well.ReadOnlyReentrancy.t.sol |
| ./test/Well.RemoveLiquidity.t.sol |
| ./test/Well.RemoveLiquidityImbalanced.t.sol |
| ./test/Well.RemoveLiquidityOneToken.t.sol |
| ./test/Well.Shift.t.sol |
| ./test/Well.Skim.t.sol |
| ./test/Well.SucceedOnPumpFailure.t.sol |
| ./test/Well.SwapFrom.t.sol |
| ./test/Well.SwapFromFeeOnTransfer.Fee.t.sol |
| ./test/Well.SwapFromFeeOnTransfer.NoFee.t.sol |
| ./test/Well.SwapTo.t.sol |
| ./test/Well.Sync.t.sol |
| ./test/Well.Tokens.t.sol |
| ./test/Well.UpdatePump.t.sol |
| ./test/WellUpgradeable.t.sol |
| ./test/beanstalk/BeanstalkConstantProduct.calcReserveAtRatioLiquidity.t.sol |
| ./test/beanstalk/BeanstalkConstantProduct.calcReserveAtRatioSwap.t.sol |
| ./test/beanstalk/BeanstalkConstantProduct2.calcReserveAtRatioLiquidity.t.sol |
| ./test/beanstalk/BeanstalkConstantProduct2.calcReserveAtRatioSwap.t.sol |
| ./test/beanstalk/BeanstalkStable2.calcReserveAtRatioLiquidity.t.sol |
| ./test/beanstalk/BeanstalkStable2.calcReserveAtRatioSwap.t.sol |
| ./test/functions/ConstantProduct.t.sol |
| ./test/functions/ConstantProduct2.t.sol |
| ./test/functions/Stable2.t.sol |
| ./test/functions/WellFunctionHelper.sol |
| ./test/helpers/Users.sol |
| ./test/integration/GasMetering.sol |
| ./test/integration/IntegrationTestGasComparisons.sol |
| ./test/integration/IntegrationTestHelper.sol |
| ./test/integration/interfaces/ICurve.sol |
| ./test/integration/interfaces/IPipeline.sol |
| ./test/integration/interfaces/IUniswap.sol |
| ./test/invariant/Handler.t.sol |
| ./test/invariant/Invariants.t.sol |
| ./test/libraries/LibBytes.t.sol |
| ./test/libraries/LibBytes16.t.sol |
| ./test/libraries/LibContractInfo.t.sol |
| ./test/libraries/LibLastReserveBytes.t.sol |
| ./test/libraries/LibMath.t.sol |
| ./test/libraries/TestABDK.t.sol |
| ./test/pumps/Pump.CapReserves.t.sol |
| ./test/pumps/Pump.Fuzz.t.sol |
| ./test/pumps/Pump.Helpers.t.sol |
| ./test/pumps/Pump.Longevity.t.sol |
| ./test/pumps/Pump.NotInitialized.t.sol |
| ./test/pumps/Pump.TimeWeightedAverage.t.sol |
| ./test/pumps/Pump.Update.t.sol |
| ./test/pumps/PumpHelpers.sol |
| Totals: 117 |

## Scoping Q &amp; A

### General questions


| Question                                | Answer                       |
| --------------------------------------- | ---------------------------- |
| ERC20 used by the protocol              |       Any (all possible ERC20s)             |
| Test coverage                           | Lines: 81.80% - Functions: 81.19%                           |
| ERC721 used  by the protocol            |            None              |
| ERC777 used by the protocol             |           None                |
| ERC1155 used by the protocol            |              None            |
| Chains the protocol will be deployed on | Ethereum |

### ERC20 token behaviors in scope

| Question                                                                                                                                                   | Answer |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| [Missing return values](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#missing-return-values)                                                      |   Out of scope  |
| [Fee on transfer](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#fee-on-transfer)                                                                  |  Out of scope  |
| [Balance changes outside of transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#balance-modifications-outside-of-transfers-rebasingairdrops) | Out of scope    |
| [Upgradeability](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#upgradable-tokens)                                                                 |   In scope  |
| [Flash minting](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#flash-mintable-tokens)                                                              | Out of scope    |
| [Pausability](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#pausable-tokens)                                                                      | Out of scope    |
| [Approval race protections](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#approval-race-protections)                                              | Out of scope    |
| [Revert on approval to zero address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-approval-to-zero-address)                            | Out of scope    |
| [Revert on zero value approvals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-approvals)                                    | Out of scope    |
| [Revert on zero value transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers)                                    | Out of scope    |
| [Revert on transfer to the zero address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-transfer-to-the-zero-address)                    | Out of scope    |
| [Revert on large approvals and/or transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-large-approvals--transfers)                  | Out of scope    |
| [Doesn't revert on failure](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#no-revert-on-failure)                                                   |  Out of scope   |
| [Multiple token addresses](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers)                                          | Out of scope    |
| [Low decimals ( < 6)](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#low-decimals)                                                                 |   Out of scope  |
| [High decimals ( > 18)](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#high-decimals)                                                              | Out of scope    |
| [Blocklists](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#tokens-with-blocklists)                                                                | Out of scope    |

### External integrations (e.g., Uniswap) behavior in scope:


| Question                                                  | Answer |
| --------------------------------------------------------- | ------ |
| Enabling/disabling fees (e.g. Blur disables/enables fees) | No   |
| Pausability (e.g. Uniswap pool gets paused)               |  No   |
| Upgradeability (e.g. Uniswap gets upgraded)               |   No  |


### EIP compliance
`src/WellUpgradeable.sol`: should comply with EIP-1822



# Additional context

## Main invariants

None

## Attack ideas (where to focus for bugs)
None

## All trusted roles in the protocol

N/A


## Describe any novel or unique curve logic or mathematical models implemented in the contracts:

With regard to the Stable 2 Well Function, a lookup table is used to assist the Newtonian estimation to decrease the computation needed to converge to an answer. See in line comments.

## Running tests

Setup the repo and requirements:
```bash
git clone https://github.com/code-423n4/2024-07-basin.git
cd 2024-07-basin
git submodule update --init --recursive
foundryup
forge install
```
Setup Python environment and perform the tests (Make sure your `MAINNET_RPC_URL` is set in `.env` file):
```bash
python3 -m venv env 
source env/bin/activate 
python3 -m pip install -r requirements.txt
forge test --ffi
```
To run code coverage:
```bash
forge coverage --ffi
```

| File                                                            | % Lines            | % Statements       | % Branches         | % Funcs          |
|-----------------------------------------------------------------|--------------------|--------------------|--------------------|------------------|
| mocks/functions/MockEmptyFunction.sol                           | 66.67% (2/3)       | 66.67% (2/3)       | 100.00% (0/0)      | 80.00% (4/5)     |
| mocks/functions/MockFunctionBad.sol                             | 33.33% (1/3)       | 25.00% (1/4)       | 100.00% (0/0)      | 60.00% (3/5)     |
| mocks/pumps/MockFailPump.sol                                    | 100.00% (1/1)      | 100.00% (1/1)      | 100.00% (0/0)      | 100.00% (1/1)    |
| mocks/pumps/MockPump.sol                                        | 50.00% (1/2)       | 50.00% (1/2)       | 100.00% (0/0)      | 50.00% (1/2)     |
| mocks/tokens/MockToken.sol                                      | 83.33% (5/6)       | 83.33% (5/6)       | 100.00% (0/0)      | 80.00% (4/5)     |
| mocks/tokens/MockTokenFeeOnTransfer.sol                         | 81.25% (13/16)     | 86.36% (19/22)     | 100.00% (0/0)      | 66.67% (6/9)     |
| mocks/tokens/ReentrantMockToken.sol                             | 100.00% (7/7)      | 88.89% (8/9)       | 100.00% (6/6)      | 100.00% (3/3)    |
| mocks/wells/MockInitFailWell.sol                                | 100.00% (2/2)      | 100.00% (2/2)      | 100.00% (0/0)      | 100.00% (2/2)    |
| mocks/wells/MockReserveWell.sol                                 | 100.00% (7/7)      | 100.00% (7/7)      | 100.00% (0/0)      | 100.00% (6/6)    |
| mocks/wells/MockStaticWell.sol                                  | 100.00% (31/31)    | 100.00% (40/40)    | 100.00% (4/4)      | 100.00% (10/10)  |
| mocks/wells/MockWellUpgradeable.sol                             | 100.00% (1/1)      | 100.00% (1/1)      | 100.00% (0/0)      | 100.00% (1/1)    |
| script/deploy/Aquifer.s.sol                                     | 0.00% (0/3)        | 0.00% (0/4)        | 100.00% (0/0)      | 0.00% (0/1)      |
| script/deploy/AquiferWell.s.sol                                 | 0.00% (0/17)       | 0.00% (0/23)       | 100.00% (0/0)      | 0.00% (0/1)      |
| script/deploy/MockPump.s.sol                                    | 0.00% (0/5)        | 0.00% (0/7)        | 100.00% (0/0)      | 0.00% (0/1)      |
| script/deploy/Well.s.sol                                        | 0.00% (0/17)       | 0.00% (0/23)       | 100.00% (0/0)      | 0.00% (0/1)      |
| script/deploy/helpers/Logger.sol                                | 0.00% (0/8)        | 0.00% (0/8)        | 100.00% (0/0)      | 0.00% (0/1)      |
| script/helpers/WellDeployer.sol                                 | 100.00% (6/6)      | 100.00% (6/6)      | 100.00% (0/0)      | 100.00% (2/2)    |
| script/simulations/stableswap/StableswapCalcRatiosLiqSim.s.sol  | 0.00% (0/43)       | 0.00% (0/55)       | 100.00% (0/0)      | 0.00% (0/1)      |
| script/simulations/stableswap/StableswapCalcRatiosSwapSim.s.sol | 0.00% (0/57)       | 0.00% (0/75)       | 100.00% (0/0)      | 0.00% (0/1)      |
| src/Aquifer.sol                                                 | 100.00% (27/27)    | 100.00% (30/30)    | 100.00% (20/20)    | 66.67% (2/3)     |
| src/Well.sol                                                    | 98.84% (255/258)   | 98.65% (365/370)   | 100.00% (52/52)    | 95.92% (47/49)   |
| src/WellUpgradeable.sol                                         | 83.33% (25/30)     | 86.05% (37/43)     | 85.71% (12/14)     | 80.00% (8/10)    |
| src/functions/ConstantProduct.sol                               | 77.27% (17/22)     | 70.59% (24/34)     | 66.67% (4/6)       | 75.00% (6/8)     |
| src/functions/ConstantProduct2.sol                              | 100.00% (12/12)    | 100.00% (16/16)    | 100.00% (2/2)      | 100.00% (7/7)    |
| src/functions/ProportionalLPToken.sol                           | 0.00% (0/3)        | 0.00% (0/5)        | 100.00% (0/0)      | 0.00% (0/1)      |
| src/functions/ProportionalLPToken2.sol                          | 100.00% (3/3)      | 100.00% (3/3)      | 100.00% (0/0)      | 100.00% (1/1)    |
| src/functions/Stable2.sol                                       | 92.11% (105/114)   | 92.70% (165/178)   | 84.78% (39/46)     | 85.71% (12/14)   |
| src/functions/StableLUT/Stable2LUT1.sol                         | 94.84% (386/407)   | 94.84% (386/407)   | 94.80% (383/404)   | 100.00% (3/3)    |
| src/libraries/ABDKMathQuad.sol                                  | 73.26% (778/1062)  | 73.37% (1149/1566) | 77.16% (696/902)   | 46.88% (15/32)   |
| src/libraries/LibBytes.sol                                      | 100.00% (26/26)    | 100.00% (33/33)    | 100.00% (18/18)    | 100.00% (2/2)    |
| src/libraries/LibBytes16.sol                                    | 100.00% (21/21)    | 100.00% (28/28)    | 100.00% (8/8)      | 100.00% (2/2)    |
| src/libraries/LibClone.sol                                      | 88.66% (86/97)     | 88.89% (88/99)     | 80.00% (4/5)       | 90.00% (9/10)    |
| src/libraries/LibContractInfo.sol                               | 66.67% (8/12)      | 61.54% (8/13)      | 50.00% (2/4)       | 66.67% (2/3)     |
| src/libraries/LibLastReserveBytes.sol                           | 97.56% (40/41)     | 98.18% (54/55)     | 100.00% (14/14)    | 75.00% (3/4)     |
| src/libraries/LibMath.sol                                       | 98.53% (67/68)     | 96.59% (85/88)     | 100.00% (24/24)    | 100.00% (4/4)    |
| src/libraries/LibWellConstructor.sol                            | 92.86% (13/14)     | 94.74% (18/19)     | 100.00% (0/0)      | 75.00% (3/4)     |
| src/libraries/LibWellUpgradeableConstructor.sol                 | 92.86% (13/14)     | 94.74% (18/19)     | 100.00% (0/0)      | 75.00% (3/4)     |
| src/pumps/MultiFlowPump.sol                                     | 96.45% (190/197)   | 96.39% (267/277)   | 96.15% (50/52)     | 100.00% (21/21)  |
| src/utils/Clone.sol                                             | 41.67% (5/12)      | 38.89% (7/18)      | 100.00% (0/0)      | 50.00% (3/6)     |
| src/utils/ClonePlus.sol                                         | 100.00% (7/7)      | 100.00% (12/12)    | 100.00% (2/2)      | 100.00% (2/2)    |
| test/LiquidityHelper.sol                                        | 63.16% (24/38)     | 67.80% (40/59)     | 100.00% (0/0)      | 57.14% (4/7)     |
| test/SwapHelper.sol                                             | 92.31% (24/26)     | 94.29% (33/35)     | 100.00% (2/2)      | 66.67% (2/3)     |
| test/TestHelper.sol                                             | 89.29% (150/168)   | 90.31% (205/227)   | 88.89% (16/18)     | 86.96% (40/46)   |
| test/helpers/Users.sol                                          | 81.82% (9/11)      | 81.25% (13/16)     | 100.00% (0/0)      | 66.67% (2/3)     |
| test/integration/IntegrationTestHelper.sol                      | 93.55% (29/31)     | 92.68% (38/41)     | 100.00% (2/2)      | 100.00% (6/6)    |
| test/invariant/Handler.t.sol                                    | 89.96% (233/259)   | 90.29% (316/350)   | 100.00% (36/36)    | 90.91% (20/22)   |
| Total                                                           | 81.80% (2630/3215) | 81.38% (3531/4339) | 85.07% (1396/1641) | 81.19% (272/335) |

To run gas benchmarks:
```bash
forge test --ffi --gas-report
```



## Miscellaneous
Employees of Beanstalk Farms contributors and employees' family members are ineligible to participate in this audit.
