# Report

## Low Issues


| |Issue|Instances|
|-|:-|:-:|
| [L-1](#L-1) | Use a 2-step ownership transfer pattern | 1 |
| [L-2](#L-2) | Precision Loss due to Division before Multiplication | 1 |
| [L-3](#L-3) | `decimals()` should be of type `uint8` | 2 |
| [L-4](#L-4) | Division by zero not prevented | 15 |
| [L-5](#L-5) | Initializers could be front-run | 7 |
| [L-6](#L-6) | Possible rounding issue | 6 |
| [L-7](#L-7) | Loss of precision | 4 |
| [L-8](#L-8) | Solidity version 0.8.20+ may not work on other chains due to `PUSH0` | 3 |
| [L-9](#L-9) | Use `Ownable2Step.transferOwnership` instead of `Ownable.transferOwnership` | 1 |
| [L-10](#L-10) | Upgradeable contract is missing a `__gap[50]` storage variable to allow for new storage variables in later versions | 6 |
| [L-11](#L-11) | Upgradeable contract not initialized | 14 |
### <a name="L-1"></a>[L-1] Use a 2-step ownership transfer pattern
Recommend considering implementing a two step process where the owner or admin nominates an account and the nominated account needs to call an `acceptOwnership()` function for the transfer of ownership to fully succeed. This ensures the nominated EOA account is a valid and active account. Lack of two-step procedure for critical operations leaves them error-prone. Consider adding two step procedure on the critical functions.

*Instances (1)*:
```solidity
File: ./src/WellUpgradeable.sol

16: contract WellUpgradeable is Well, UUPSUpgradeable, OwnableUpgradeable {

```

### <a name="L-2"></a>[L-2] Precision Loss due to Division before Multiplication
division operations can lead to a loss of precision as the fractional part is discarded. When the result of such a division operation is then multiplied, this loss of precision can be magnified, potentially leading to significant inaccuracies in the calculations.

*Instances (1)*:
```solidity
File: ./src/functions/Stable2.sol

380:         c = lpTokenSupply * lpTokenSupply / (reserves * N) * lpTokenSupply * A_PRECISION / (Ann * N);

```

### <a name="L-3"></a>[L-3] `decimals()` should be of type `uint8`

*Instances (2)*:
```solidity
File: ./src/functions/Stable2.sol

310:     function decodeWellData(bytes memory data) public view virtual returns (uint256[] memory decimals) {

359:         uint256[] memory decimals

```

### <a name="L-4"></a>[L-4] Division by zero not prevented
The divisions below take an input parameter which does not have any zero-value checks, which may lead to the functions reverting when zero is passed.

*Instances (15)*:
```solidity
File: ./src/functions/Stable2.sol

91:             dP = dP * lpTokenSupply / (scaledReserves[0] * N);

92:             dP = dP * lpTokenSupply / (scaledReserves[1] * N);

94:             lpTokenSupply = (Ann * sumReserves / A_PRECISION + (dP * N)) * lpTokenSupply

135:                     return reserve / (10 ** (18 - decimals[j]));

139:                     return reserve / (10 ** (18 - decimals[j]));

187:         pd.targetPrice = scaledRatios[i] * PRICE_PRECISION / scaledRatios[j];

201:             scaledReserves[i] = parityReserve * pd.lutData.lowPriceI / pd.lutData.precision;

231:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

235:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

260:         pd.targetPrice = scaledRatios[i] * PRICE_PRECISION / scaledRatios[j];

296:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

300:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

372:         return (reserve * reserve + c) / (reserve * 2 + b - lpTokenSupply);

380:         c = lpTokenSupply * lpTokenSupply / (reserves * N) * lpTokenSupply * A_PRECISION / (Ann * N);

392:                 - pd.maxStepSize * (pd.targetPrice - pd.currentPrice) / (pd.lutData.highPrice - pd.lutData.lowPrice);

```

### <a name="L-5"></a>[L-5] Initializers could be front-run
Initializers could be front-run, allowing an attacker to either set their own values, take ownership of the contract, and in the best case forcing a re-deployment

*Instances (7)*:
```solidity
File: ./src/WellUpgradeable.sol

33:     function init(string memory _name, string memory _symbol) external override reinitializer(2) {

34:         __ERC20Permit_init(_name);

35:         __ERC20_init(_name, _symbol);

36:         __ReentrancyGuard_init();

37:         __UUPSUpgradeable_init();

38:         __Ownable_init();

54:     function initNoWellToken() external initializer {}

```

### <a name="L-6"></a>[L-6] Possible rounding issue
Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator. Also, there is indication of multiplication and division without the use of parenthesis which could result in issues.

*Instances (6)*:
```solidity
File: ./src/functions/Stable2.sol

91:             dP = dP * lpTokenSupply / (scaledReserves[0] * N);

92:             dP = dP * lpTokenSupply / (scaledReserves[1] * N);

94:             lpTokenSupply = (Ann * sumReserves / A_PRECISION + (dP * N)) * lpTokenSupply

95:                 / (((Ann - A_PRECISION) * lpTokenSupply / A_PRECISION) + ((N + 1) * dP));

372:         return (reserve * reserve + c) / (reserve * 2 + b - lpTokenSupply);

380:         c = lpTokenSupply * lpTokenSupply / (reserves * N) * lpTokenSupply * A_PRECISION / (Ann * N);

```

### <a name="L-7"></a>[L-7] Loss of precision
Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator

*Instances (4)*:
```solidity
File: ./src/functions/Stable2.sol

94:             lpTokenSupply = (Ann * sumReserves / A_PRECISION + (dP * N)) * lpTokenSupply

95:                 / (((Ann - A_PRECISION) * lpTokenSupply / A_PRECISION) + ((N + 1) * dP));

372:         return (reserve * reserve + c) / (reserve * 2 + b - lpTokenSupply);

380:         c = lpTokenSupply * lpTokenSupply / (reserves * N) * lpTokenSupply * A_PRECISION / (Ann * N);

```

### <a name="L-8"></a>[L-8] Solidity version 0.8.20+ may not work on other chains due to `PUSH0`
The compiler for Solidity 0.8.20 switches the default target EVM version to [Shanghai](https://blog.soliditylang.org/2023/05/10/solidity-0.8.20-release-announcement/#important-note), which includes the new `PUSH0` op code. This op code may not yet be implemented on all L2s, so deployment on these chains will fail. To work around this issue, use an earlier [EVM](https://docs.soliditylang.org/en/v0.8.20/using-the-compiler.html?ref=zaryabs.com#setting-the-evm-version-to-target) [version](https://book.getfoundry.sh/reference/config/solidity-compiler#evm_version). While the project itself may or may not compile with 0.8.20, other projects with which it integrates, or which extend this project may, and those projects will have problems deploying these contracts/libraries.

*Instances (3)*:
```solidity
File: ./src/WellUpgradeable.sol

3: pragma solidity ^0.8.20;

```

```solidity
File: ./src/functions/Stable2.sol

3: pragma solidity ^0.8.20;

```

```solidity
File: ./src/functions/StableLUT/Stable2LUT1.sol

3: pragma solidity ^0.8.20;

```

### <a name="L-9"></a>[L-9] Use `Ownable2Step.transferOwnership` instead of `Ownable.transferOwnership`
Use [Ownable2Step.transferOwnership](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol) which is safer. Use it as it is more secure due to 2-stage ownership transfer.

**Recommended Mitigation Steps**

Use <a href="https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol">Ownable2Step.sol</a>
  
  ```solidity
      function acceptOwnership() external {
          address sender = _msgSender();
          require(pendingOwner() == sender, "Ownable2Step: caller is not the new owner");
          _transferOwnership(sender);
      }
```

*Instances (1)*:
```solidity
File: ./src/WellUpgradeable.sol

7: import {OwnableUpgradeable} from "ozu/access/OwnableUpgradeable.sol";

```

### <a name="L-10"></a>[L-10] Upgradeable contract is missing a `__gap[50]` storage variable to allow for new storage variables in later versions
See [this](https://docs.openzeppelin.com/contracts/4.x/upgradeable#storage_gaps) link for a description of this storage variable. While some contracts may not currently be sub-classed, adding the variable now protects against forgetting to add it in the future.

*Instances (6)*:
```solidity
File: ./src/WellUpgradeable.sol

6: import {UUPSUpgradeable} from "ozu/proxy/utils/UUPSUpgradeable.sol";

7: import {OwnableUpgradeable} from "ozu/access/OwnableUpgradeable.sol";

16: contract WellUpgradeable is Well, UUPSUpgradeable, OwnableUpgradeable {

28:             revert("UUPSUpgradeable: must not be called through delegatecall");

37:         __UUPSUpgradeable_init();

82:             UUPSUpgradeable(newImplmentation).proxiableUUID() == _IMPLEMENTATION_SLOT,

```

### <a name="L-11"></a>[L-11] Upgradeable contract not initialized
Upgradeable contracts are initialized via an initializer function rather than by a constructor. Leaving such a contract uninitialized may lead to it being taken over by a malicious user

*Instances (14)*:
```solidity
File: ./src/WellUpgradeable.sol

6: import {UUPSUpgradeable} from "ozu/proxy/utils/UUPSUpgradeable.sol";

7: import {OwnableUpgradeable} from "ozu/access/OwnableUpgradeable.sol";

16: contract WellUpgradeable is Well, UUPSUpgradeable, OwnableUpgradeable {

28:             revert("UUPSUpgradeable: must not be called through delegatecall");

33:     function init(string memory _name, string memory _symbol) external override reinitializer(2) {

34:         __ERC20Permit_init(_name);

35:         __ERC20_init(_name, _symbol);

36:         __ReentrancyGuard_init();

37:         __UUPSUpgradeable_init();

38:         __Ownable_init();

54:     function initNoWellToken() external initializer {}

82:             UUPSUpgradeable(newImplmentation).proxiableUUID() == _IMPLEMENTATION_SLOT,

130:     function getInitializerVersion() external view returns (uint256) {

131:         return _getInitializedVersion();

```
