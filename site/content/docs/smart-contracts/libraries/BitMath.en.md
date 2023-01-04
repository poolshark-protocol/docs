This library provides functionality for computing bit properties of an unsigned integer

## Functions

### mostSignificantBit

```solidity
  function mostSignificantBit(
    uint256 value
  ) internal pure returns (uint8 index)
```

Returns the index of the most significant bit of the number,
where the least significant bit is at index 0 (i.e. rightmost bit) and the most significant bit is at index 255 (i.e. leftmost bit).

#### Parameters:

| Name | Type    | Description                                                                     |
| :--- | :------ | :------------------------------------------------------------------------------ |
| `value`  | uint256 | the value for which to compute the most significant bit, must be greater than 0 |

#### Return Values:

| Name | Type  | Description                           |
| :--- | :---- | :------------------------------------ |
| `index`  | unit8 | the index of the most significant bit |

### leastSignificantBit

```solidity
  function leastSignificantBit(
    uint256 value
  ) internal pure returns (uint8 index)
```

Returns the index of the least significant bit of the number,
where the least significant bit is at index 0 (i.e. rightmost bit) and the most significant bit is at index 255 (i.e. leftmost bit).

#### Parameters:

| Name | Type    | Description                                                                      |
| :--- | :------ | :------------------------------------------------------------------------------- |
| `value`  | uint256 | the value for which to compute the least significant bit, must be greater than 0 |

#### Return Values:

| Name | Type  | Description                            |
| :--- | :---- | :------------------------------------- |
| `index`  | unit8 | the index of the least significant bit |
