Facilitates multiplication and division that can have overflow of an intermediate value without any loss of precision.                                                                                                                     

Handles "phantom overflow" and prevents overflow of 256 bits in intermediate values between the multiplication and division steps.

## Functions

### safeMulDiv

```solidity
  function safeMulDiv(
    uint256 value,
    uint256 multiplier,
    uint256 denominator
  ) internal pure returns (uint256 result)
```

Calculates floor(value×multiplier÷denominator) with maximum precision. Reverts if `result` overflows a uint256 or `denominator` == 0.

Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv.

#### Parameters:

| Name          | Type    | Description      |
| :------------ | :------ | :--------------- |
| `value`       | uint256 | The multiplicand |
| `multiplier`  | uint256 | The multiplier   |
| `denominator` | uint256 | The divisor      |

#### Return Values:

| Name     | Type    | Description        |
| :------- | :------ | :----------------- |
| `result` | uint256 | The 256-bit result |

### safeMulDivCeiling

```solidity
  function safeMulDivCeiling(
    uint256 initial,
    uint256 b,
    uint256 denominator
  ) internal pure returns (uint256 result)
```

Calculates ceil(a×b÷denominator) with full precision. Throws if result overflows a uint256 or denominator == 0

#### Parameters:

| Name          | Type    | Description      |
| :------------ | :------ | :--------------- |
| `value`       | uint256 | The multiplicand |
| `multiplier`  | uint256 | The multiplier   |
| `denominator` | uint256 | The divisor      |

#### Return Values:

| Name     | Type    | Description        |
| :------- | :------ | :----------------- |
| `result` | uint256 | The 256-bit result |
