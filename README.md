# ✨ So you want to run an audit

This `README.md` contains a set of checklists for our audit collaboration.

Your audit will use two repos: 
- **an _audit_ repo** (this one), which is used for scoping your audit and for providing information to wardens
- **a _findings_ repo**, where issues are submitted (shared with you after the audit) 

Ultimately, when we launch the audit, this repo will be made public and will contain the smart contracts to be reviewed and all the information needed for audit participants. The findings repo will be made public after the audit report is published and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the audit sponsor (⭐️)**.

---

# Audit setup

## 🐺 C4: Set up repos
- [ ] Create a new private repo named `YYYY-MM-sponsorname` using this repo as a template.
- [ ] Rename this repo to reflect audit date (if applicable)
- [ ] Rename audit H1 below
- [ ] Update pot sizes
  - [ ] Remove the "Bot race findings opt out" section if there's no bot race.
- [ ] Fill in start and end times in audit bullets below
- [ ] Add link to submission form in audit details below
- [ ] Add the information from the scoping form to the "Scoping Details" section at the bottom of this readme.
- [ ] Add matching info to the Code4rena site
- [ ] Add sponsor to this private repo with 'maintain' level access.
- [ ] Send the sponsor contact the url for this repo to follow the instructions below and add contracts here. 
- [ ] Delete this checklist.

# Repo setup

## ⭐️ Sponsor: Add code to this repo

- [ ] Create a PR to this repo with the below changes:
- [ ] Confirm that this repo is a self-contained repository with working commands that will build (at least) all in-scope contracts, and commands that will run tests producing gas reports for the relevant contracts.
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 48 business hours prior to audit start time.**
- [ ] Be prepared for a 🚨code freeze🚨 for the duration of the audit — important because it establishes a level playing field. We want to ensure everyone's looking at the same code, no matter when they look during the audit. (Note: this includes your own repo, since a PR can leak alpha to our wardens!)

## ⭐️ Sponsor: Repo checklist

- [ ] Modify the [Overview](#overview) section of this `README.md` file. Describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the auditors should keep in mind when reviewing. (Here are two well-constructed examples: [Ajna Protocol](https://github.com/code-423n4/2023-05-ajna) and [Maia DAO Ecosystem](https://github.com/code-423n4/2023-05-maia))
- [ ] Review the Gas award pool amount, if applicable. This can be adjusted up or down, based on your preference - just flag it for Code4rena staff so we can update the pool totals across all comms channels.
- [ ] Optional: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
- [ ] [This checklist in Notion](https://code4rena.notion.site/Key-info-for-Code4rena-sponsors-f60764c4c4574bbf8e7a6dbd72cc49b4#0cafa01e6201462e9f78677a39e09746) provides some best practices for Code4rena audit repos.

## ⭐️ Sponsor: Final touches
- [ ] Review and confirm the pull request created by the Scout (technical reviewer) who was assigned to your contest. *Note: any files not listed as "in scope" will be considered out of scope for the purposes of judging, even if the file will be part of the deployed contracts.*
- [ ] Check that images and other files used in this README have been uploaded to the repo as a file and then linked in the README using absolute path (e.g. `https://github.com/code-423n4/yourrepo-url/filepath.png`)
- [ ] Ensure that *all* links and image/file paths in this README use absolute paths, not relative paths
- [ ] Check that all README information is in markdown format (HTML does not render on Code4rena.com)
- [ ] Delete this checklist and all text above the line below when you're ready.

---

# Basin audit details
- Total Prize Pool: $37500 in USDC
  - HM awards: $23520 in USDC
  - (remove this line if there is no Analysis pool) Analysis awards: XXX XXX USDC (Notion: Analysis pool)
  - QA awards: $980 in USDC
  - (remove this line if there is no Bot race) Bot Race awards: XXX XXX USDC (Notion: Bot Race pool)
 
  - Judge awards: $4500 in USDC
  - Validator awards: XXX XXX USDC (Notion: Triage fee - final)
  - Scout awards: $500 in USDC
  - (this line can be removed if there is no mitigation) Mitigation Review: XXX XXX USDC (*Opportunity goes to top 3 backstage wardens based on placement in this audit who RSVP.*)
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2024-07-basin/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts July 29, 2024 20:00 UTC
- Ends August 8, 2024 20:00 UTC

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2024-07-basin/blob/main/4naly3er-report.md).



_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._
## 🐺 C4: Begin Gist paste here (and delete this line)





# Scope

*See [scope.txt](https://github.com/code-423n4/2024-07-basin/blob/main/scope.txt)*

### Files in scope


| File   | Logic Contracts | Interfaces | nSLOC | Purpose | Libraries used |
| ------ | --------------- | ---------- | ----- | -----   | ------------ |
| /src/functions/Stable2.sol | 1| **** | 194 | |src/interfaces/IBeanstalkWellFunction.sol<br>src/interfaces/ILookupTable.sol<br>src/functions/ProportionalLPToken2.sol<br>forge-std/interfaces/IERC20.sol|
| /src/functions/StableLUT/Stable2LUT1.sol | 1| **** | 2150 | |src/interfaces/ILookupTable.sol|
| /src/WellUpgradeable.sol | 1| **** | 70 | |src/Well.sol<br>ozu/proxy/utils/UUPSUpgradeable.sol<br>ozu/access/OwnableUpgradeable.sol<br>oz/token/ERC20/utils/SafeERC20.sol<br>src/interfaces/IAquifer.sol|
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

