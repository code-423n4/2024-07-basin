
# Basin audit details
- Total Prize Pool: $37,500 in USDC
  - HM awards: $23,520 in USDC
  - QA awards: $980 in USDC 
  - Judge awards: $4,500 in USDC
  - Validator awards: $2,000 in USDC
  - Scout awards: $500 in USDC
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

[ ⭐️ SPONSORS: add info here ]

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
| [/src/functions/Stable2.sol](https://github.com/code-423n4/2024-07-basin/blob/main/src/functions/Stable2.sol) | 1| **** | 194 | |src/interfaces/IBeanstalkWellFunction.sol<br>src/interfaces/ILookupTable.sol<br>src/functions/ProportionalLPToken2.sol<br>forge-std/interfaces/IERC20.sol|
| [/src/functions/StableLUT/Stable2LUT1.sol](https://github.com/code-423n4/2024-07-basin/blob/main/src/functions/StableLUT/Stable2LUT1.sol) | 1| **** | 2150 | |src/interfaces/ILookupTable.sol|
| [/src/WellUpgradeable.sol](https://github.com/code-423n4/2024-07-basin/blob/main/src/WellUpgradeable.sol) | 1| **** | 70 | |src/Well.sol<br>ozu/proxy/utils/UUPSUpgradeable.sol<br>ozu/access/OwnableUpgradeable.sol<br>oz/token/ERC20/utils/SafeERC20.sol<br>src/interfaces/IAquifer.sol|
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


### EIP compliance checklist
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

<pre>| File                                                            | % Lines            | % Statements       | % Branches         | % Funcs          |
|-----------------------------------------------------------------|--------------------|--------------------|--------------------|------------------|
| mocks/functions/MockEmptyFunction.sol                           |<font color="#E9AD0C"> 66.67% (2/3)       </font>|<font color="#E9AD0C"> 66.67% (2/3)       </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 80.00% (4/5)     </font>|
| mocks/functions/MockFunctionBad.sol                             |<font color="#F66151"> 33.33% (1/3)       </font>|<font color="#F66151"> 25.00% (1/4)       </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#E9AD0C"> 60.00% (3/5)     </font>|
| mocks/pumps/MockFailPump.sol                                    |<font color="#33DA7A"> 100.00% (1/1)      </font>|<font color="#33DA7A"> 100.00% (1/1)      </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 100.00% (1/1)    </font>|
| mocks/pumps/MockPump.sol                                        |<font color="#E9AD0C"> 50.00% (1/2)       </font>|<font color="#E9AD0C"> 50.00% (1/2)       </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#E9AD0C"> 50.00% (1/2)     </font>|
| mocks/tokens/MockToken.sol                                      |<font color="#33DA7A"> 83.33% (5/6)       </font>|<font color="#33DA7A"> 83.33% (5/6)       </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 80.00% (4/5)     </font>|
| mocks/tokens/MockTokenFeeOnTransfer.sol                         |<font color="#33DA7A"> 81.25% (13/16)     </font>|<font color="#33DA7A"> 86.36% (19/22)     </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#E9AD0C"> 66.67% (6/9)     </font>|
| mocks/tokens/ReentrantMockToken.sol                             |<font color="#33DA7A"> 100.00% (7/7)      </font>|<font color="#33DA7A"> 88.89% (8/9)       </font>|<font color="#33DA7A"> 100.00% (6/6)      </font>|<font color="#33DA7A"> 100.00% (3/3)    </font>|
| mocks/wells/MockInitFailWell.sol                                |<font color="#33DA7A"> 100.00% (2/2)      </font>|<font color="#33DA7A"> 100.00% (2/2)      </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 100.00% (2/2)    </font>|
| mocks/wells/MockReserveWell.sol                                 |<font color="#33DA7A"> 100.00% (7/7)      </font>|<font color="#33DA7A"> 100.00% (7/7)      </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 100.00% (6/6)    </font>|
| mocks/wells/MockStaticWell.sol                                  |<font color="#33DA7A"> 100.00% (31/31)    </font>|<font color="#33DA7A"> 100.00% (40/40)    </font>|<font color="#33DA7A"> 100.00% (4/4)      </font>|<font color="#33DA7A"> 100.00% (10/10)  </font>|
| mocks/wells/MockWellUpgradeable.sol                             |<font color="#33DA7A"> 100.00% (1/1)      </font>|<font color="#33DA7A"> 100.00% (1/1)      </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 100.00% (1/1)    </font>|
| script/deploy/Aquifer.s.sol                                     |<font color="#F66151"> 0.00% (0/3)        </font>|<font color="#F66151"> 0.00% (0/4)        </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#F66151"> 0.00% (0/1)      </font>|
| script/deploy/AquiferWell.s.sol                                 |<font color="#F66151"> 0.00% (0/17)       </font>|<font color="#F66151"> 0.00% (0/23)       </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#F66151"> 0.00% (0/1)      </font>|
| script/deploy/MockPump.s.sol                                    |<font color="#F66151"> 0.00% (0/5)        </font>|<font color="#F66151"> 0.00% (0/7)        </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#F66151"> 0.00% (0/1)      </font>|
| script/deploy/Well.s.sol                                        |<font color="#F66151"> 0.00% (0/17)       </font>|<font color="#F66151"> 0.00% (0/23)       </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#F66151"> 0.00% (0/1)      </font>|
| script/deploy/helpers/Logger.sol                                |<font color="#F66151"> 0.00% (0/8)        </font>|<font color="#F66151"> 0.00% (0/8)        </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#F66151"> 0.00% (0/1)      </font>|
| script/helpers/WellDeployer.sol                                 |<font color="#33DA7A"> 100.00% (6/6)      </font>|<font color="#33DA7A"> 100.00% (6/6)      </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 100.00% (2/2)    </font>|
| script/simulations/stableswap/StableswapCalcRatiosLiqSim.s.sol  |<font color="#F66151"> 0.00% (0/43)       </font>|<font color="#F66151"> 0.00% (0/55)       </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#F66151"> 0.00% (0/1)      </font>|
| script/simulations/stableswap/StableswapCalcRatiosSwapSim.s.sol |<font color="#F66151"> 0.00% (0/57)       </font>|<font color="#F66151"> 0.00% (0/75)       </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#F66151"> 0.00% (0/1)      </font>|
| src/Aquifer.sol                                                 |<font color="#33DA7A"> 100.00% (27/27)    </font>|<font color="#33DA7A"> 100.00% (30/30)    </font>|<font color="#33DA7A"> 100.00% (20/20)    </font>|<font color="#E9AD0C"> 66.67% (2/3)     </font>|
| src/Well.sol                                                    |<font color="#33DA7A"> 98.84% (255/258)   </font>|<font color="#33DA7A"> 98.65% (365/370)   </font>|<font color="#33DA7A"> 100.00% (52/52)    </font>|<font color="#33DA7A"> 95.92% (47/49)   </font>|
| src/WellUpgradeable.sol                                         |<font color="#33DA7A"> 83.33% (25/30)     </font>|<font color="#33DA7A"> 86.05% (37/43)     </font>|<font color="#33DA7A"> 85.71% (12/14)     </font>|<font color="#33DA7A"> 80.00% (8/10)    </font>|
| src/functions/ConstantProduct.sol                               |<font color="#33DA7A"> 77.27% (17/22)     </font>|<font color="#E9AD0C"> 70.59% (24/34)     </font>|<font color="#E9AD0C"> 66.67% (4/6)       </font>|<font color="#33DA7A"> 75.00% (6/8)     </font>|
| src/functions/ConstantProduct2.sol                              |<font color="#33DA7A"> 100.00% (12/12)    </font>|<font color="#33DA7A"> 100.00% (16/16)    </font>|<font color="#33DA7A"> 100.00% (2/2)      </font>|<font color="#33DA7A"> 100.00% (7/7)    </font>|
| src/functions/ProportionalLPToken.sol                           |<font color="#F66151"> 0.00% (0/3)        </font>|<font color="#F66151"> 0.00% (0/5)        </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#F66151"> 0.00% (0/1)      </font>|
| src/functions/ProportionalLPToken2.sol                          |<font color="#33DA7A"> 100.00% (3/3)      </font>|<font color="#33DA7A"> 100.00% (3/3)      </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 100.00% (1/1)    </font>|
| src/functions/Stable2.sol                                       |<font color="#33DA7A"> 92.11% (105/114)   </font>|<font color="#33DA7A"> 92.70% (165/178)   </font>|<font color="#33DA7A"> 84.78% (39/46)     </font>|<font color="#33DA7A"> 85.71% (12/14)   </font>|
| src/functions/StableLUT/Stable2LUT1.sol                         |<font color="#33DA7A"> 94.84% (386/407)   </font>|<font color="#33DA7A"> 94.84% (386/407)   </font>|<font color="#33DA7A"> 94.80% (383/404)   </font>|<font color="#33DA7A"> 100.00% (3/3)    </font>|
| src/libraries/ABDKMathQuad.sol                                  |<font color="#E9AD0C"> 73.26% (778/1062)  </font>|<font color="#E9AD0C"> 73.37% (1149/1566) </font>|<font color="#33DA7A"> 77.16% (696/902)   </font>|<font color="#F66151"> 46.88% (15/32)   </font>|
| src/libraries/LibBytes.sol                                      |<font color="#33DA7A"> 100.00% (26/26)    </font>|<font color="#33DA7A"> 100.00% (33/33)    </font>|<font color="#33DA7A"> 100.00% (18/18)    </font>|<font color="#33DA7A"> 100.00% (2/2)    </font>|
| src/libraries/LibBytes16.sol                                    |<font color="#33DA7A"> 100.00% (21/21)    </font>|<font color="#33DA7A"> 100.00% (28/28)    </font>|<font color="#33DA7A"> 100.00% (8/8)      </font>|<font color="#33DA7A"> 100.00% (2/2)    </font>|
| src/libraries/LibClone.sol                                      |<font color="#33DA7A"> 88.66% (86/97)     </font>|<font color="#33DA7A"> 88.89% (88/99)     </font>|<font color="#33DA7A"> 80.00% (4/5)       </font>|<font color="#33DA7A"> 90.00% (9/10)    </font>|
| src/libraries/LibContractInfo.sol                               |<font color="#E9AD0C"> 66.67% (8/12)      </font>|<font color="#E9AD0C"> 61.54% (8/13)      </font>|<font color="#E9AD0C"> 50.00% (2/4)       </font>|<font color="#E9AD0C"> 66.67% (2/3)     </font>|
| src/libraries/LibLastReserveBytes.sol                           |<font color="#33DA7A"> 97.56% (40/41)     </font>|<font color="#33DA7A"> 98.18% (54/55)     </font>|<font color="#33DA7A"> 100.00% (14/14)    </font>|<font color="#33DA7A"> 75.00% (3/4)     </font>|
| src/libraries/LibMath.sol                                       |<font color="#33DA7A"> 98.53% (67/68)     </font>|<font color="#33DA7A"> 96.59% (85/88)     </font>|<font color="#33DA7A"> 100.00% (24/24)    </font>|<font color="#33DA7A"> 100.00% (4/4)    </font>|
| src/libraries/LibWellConstructor.sol                            |<font color="#33DA7A"> 92.86% (13/14)     </font>|<font color="#33DA7A"> 94.74% (18/19)     </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 75.00% (3/4)     </font>|
| src/libraries/LibWellUpgradeableConstructor.sol                 |<font color="#33DA7A"> 92.86% (13/14)     </font>|<font color="#33DA7A"> 94.74% (18/19)     </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#33DA7A"> 75.00% (3/4)     </font>|
| src/pumps/MultiFlowPump.sol                                     |<font color="#33DA7A"> 96.45% (190/197)   </font>|<font color="#33DA7A"> 96.39% (267/277)   </font>|<font color="#33DA7A"> 96.15% (50/52)     </font>|<font color="#33DA7A"> 100.00% (21/21)  </font>|
| src/utils/Clone.sol                                             |<font color="#F66151"> 41.67% (5/12)      </font>|<font color="#F66151"> 38.89% (7/18)      </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#E9AD0C"> 50.00% (3/6)     </font>|
| src/utils/ClonePlus.sol                                         |<font color="#33DA7A"> 100.00% (7/7)      </font>|<font color="#33DA7A"> 100.00% (12/12)    </font>|<font color="#33DA7A"> 100.00% (2/2)      </font>|<font color="#33DA7A"> 100.00% (2/2)    </font>|
| test/LiquidityHelper.sol                                        |<font color="#E9AD0C"> 63.16% (24/38)     </font>|<font color="#E9AD0C"> 67.80% (40/59)     </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#E9AD0C"> 57.14% (4/7)     </font>|
| test/SwapHelper.sol                                             |<font color="#33DA7A"> 92.31% (24/26)     </font>|<font color="#33DA7A"> 94.29% (33/35)     </font>|<font color="#33DA7A"> 100.00% (2/2)      </font>|<font color="#E9AD0C"> 66.67% (2/3)     </font>|
| test/TestHelper.sol                                             |<font color="#33DA7A"> 89.29% (150/168)   </font>|<font color="#33DA7A"> 90.31% (205/227)   </font>|<font color="#33DA7A"> 88.89% (16/18)     </font>|<font color="#33DA7A"> 86.96% (40/46)   </font>|
| test/helpers/Users.sol                                          |<font color="#33DA7A"> 81.82% (9/11)      </font>|<font color="#33DA7A"> 81.25% (13/16)     </font>|<font color="#8B8A88"> 100.00% (0/0)      </font>|<font color="#E9AD0C"> 66.67% (2/3)     </font>|
| test/integration/IntegrationTestHelper.sol                      |<font color="#33DA7A"> 93.55% (29/31)     </font>|<font color="#33DA7A"> 92.68% (38/41)     </font>|<font color="#33DA7A"> 100.00% (2/2)      </font>|<font color="#33DA7A"> 100.00% (6/6)    </font>|
| test/invariant/Handler.t.sol                                    |<font color="#33DA7A"> 89.96% (233/259)   </font>|<font color="#33DA7A"> 90.29% (316/350)   </font>|<font color="#33DA7A"> 100.00% (36/36)    </font>|<font color="#33DA7A"> 90.91% (20/22)   </font>|
| Total                                                           |<font color="#33DA7A"> 81.80% (2630/3215) </font>|<font color="#33DA7A"> 81.38% (3531/4339) </font>|<font color="#33DA7A"> 85.07% (1396/1641) </font>|<font color="#33DA7A"> 81.19% (272/335) </font>|
</pre>

To run gas benchmarks:
```bash
forge test --ffi --gas-report
```



## Miscellaneous
Employees of Basin and employees' family members are ineligible to participate in this audit.
