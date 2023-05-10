Manages range liquidity positions.

## Functions

### mint

```solidity
  function mint(
    MintParams memory params
  ) external lock

  struct MintParams {
        address to;
        int24 lower;
        int24 upper;
        uint128 amount0;
        uint128 amount1;
        bool fungible;
  }

```
Mints an ERC-1155 for the range `lower` to `upper`.

`lower` will be the lower price tick for the position.

`upper` will be the upper tick for the position.

Both `lower` and `upper` must be multiples of the `tickSpacing` for the pool.

If a `Position` is out of range, it will not collect fees.

Fees for the matching ERC-1155 id will be autocompounded when calling this function.

** Parameters: **

| Name        | Type  | Description                 |
| :---------- | :---- | :-------------------------- |
| `to` | int24 | The recipient of the fungible position |
| `lower` | int24 | The lower price tick of the range |
| `upper` | int24 | The upper price tick of the range |
| `amount0` | uint128 | The amount of `token0` to add to the `Position` |
| `amount1` | uint128 | The amount of `token1` to add to the `Position` |

** Return Values: **

| Name      | Type    | Description                                                                                                 |
| :-------- | :------ | :---------------------------------------------------------------------------------------------------------- |
| `amount0` | uint256 | The amount of token0 that was paid to mint the given amount of liquidity. Matches the value in the callback |
| `amount1` | uint256 | The amount of token1 that was paid to mint the given amount of liquidity. Matches the value in the callback |

### burn

```solidity
  function burn(
      BurnParams memory params
  ) external lock

  struct BurnParams {
      address to;
      int24 lower;
      int24 upper;
      uint128 amount;
      bool fungible;
      bool collect;
  }
```

Burn liquidity from `msg.sender`. The token received from the burned liquidity is then sent to the address `to`.

** Parameters: **

| Name        | Type    | Description                                                |
| :---------- | :------ | :--------------------------------------------------------- |
| `to` | int24   | The recipient of the token from the burned liquidity |
| `lower` | int24 | The lower price tick of the range |
| `upper` | int24 | The upper price tick of the range |
| `burnPercent` | uint128 | The percent of the user's liquidity to be burned and collected (1e38 = 100%) |

** Return Values: **

| Name      | Type    | Description                                                                                                 |
| :-------- | :------ | :---------------------------------------------------------------------------------------------------------- |
| `amount0` | uint256 | The amount of token0 that was paid to mint the given amount of liquidity. Matches the value in the callback |
| `amount1` | uint256 | The amount of token1 that was paid to mint the given amount of liquidity. Matches the value in the callback |

### swap

```solidity
  function swap(
      address recipient,
      bool zeroForOne,
      uint256 amountIn,
      uint160 priceLimit
  ) external override lock
```

Swap `token0` for `token1`, or `token1` for `token0`.

** Parameters: **

| Name                | Type    | Description                                                                                                                                                                        |
| :------------------ | :------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `recipient`         | address | The address to receive the output of the swap                                                                                                                                      |
| `zeroForOne`        | bool    | The direction of the swap, true for `token0` => `token1`, false for `token1` => `token0`                                                                                                   |
| `amountSpecified`   | int256  | The amount of the swap, which if positive is exact input, or if negative is exact output                                                                 |
| `priceLimit` | uint160 | The Q64.96 sqrt price limit. If `zeroForOne` is true, the price cannot be less than this value after the swap. If `zeroForOne` is false, the price cannot be greater than this value after the swap. |
| `data`              | bytes   | Raw data being passed through to the callback                                                                                                                                      |

** Return Values: **

| Name      | Type   | Description                                                                                |
| :-------- | :----- | :----------------------------------------------------------------------------------------- |
| `amount0` | int256 | The delta of the balance of `token0` of the pool, exact when negative, minimum when positive |
| `amount1` | int256 | The delta of the balance of `token1` of the pool, exact when negative, minimum when positive |

### increaseSampleLength

```solidity
  function increaseSampleLength(
    uint16 sampleLengthNext
  ) external override lock
```

Increase the maximum number of price and liquidity samples that can be stored by the pool.

This method will not modify state if the pool already has a `sampleLengthNext` greater than or equal to
the input `sampleLengthNext`.

** Parameters: **

| Name                         | Type   | Description                                                      |
| :--------------------------- | :----- | :--------------------------------------------------------------- |
| `observationLengthNext` | uint16 | The desired minimum number of observations for the pool to store |

### collectProtocolFees

```solidity
  function collectProtocolFees(
  ) external lock returns (
    uint128 token0Fees,
    uint128 token1Fees
  )
```

Collect the protocol fees accrued by the pool.

** Parameters: **

** Return Values: **

| Name      | Type    | Description                          |
| :-------- | :------ | :----------------------------------- |
| `token0Fees` | uint128 | The protocol fee collected in token0 |
| `token1Fees` | uint128 | The protocol fee collected in token1 |

<br/><br/>
<br/><br/>