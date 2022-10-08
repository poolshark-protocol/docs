## Functions

### \_blockTimestamp

```solidity
  function _blockTimestamp(
  ) internal view virtual returns (uint32)
```

Returns the block timestamp as a 32 bit unsigned integer.

### snapshotLiquidityInside

```solidity
  function snapshotLiquidityInside(
    int24 tickLower,
    int24 tickUpper
  ) external view override noDelegateCall returns (int56 tickCumulativeInside, uint160 secondsPerLiquidityInsideX128, uint32 secondsInside)
```
Use case: derive liquidity-in-range or time-weighted average price.

Returns a snapshot of the tick cumulative, seconds per liquidity and seconds inside the specified tick range.

This informs the caller of 
```
1) The tick * time elapsed since the pool was first initialized
2) Seconds per liquidity for the range
3) The number of seconds inside the range
```
Snapshots should only be used if the position is held for the entire period in between.

#### Parameters:

| Name        | Type  | Description                 |
| :---------- | :---- | :-------------------------- |
| `tickLower` | int24 | The lower tick of the range |
| `tickUpper` | int24 | The upper tick of the range |

#### Return Values:

| Name                            | Type    | Description                                         |
| :------------------------------ | :------ | :-------------------------------------------------- |
| `tickCumulativeInside`          | int56   | The snapshot of the tick accumulator for the range  |
| `secondsPerLiquidityInsideX128` | uint160 | The snapshot of seconds per liquidity for the range |
| `secondsInside`                 | uint32  | The snapshot of seconds per liquidity for the range |

### observe

```solidity
  function observe(
    uint32[] secondsAgos
  ) external view override noDelegateCall returns (int56[] tickCumulatives, uint160[] secondsPerLiquidityCumulativeX128s)
```

Returns an array of sample cumulative tick (tick * seconds) and liquidity (in liquidity units) as of each timestamp `secondsAgo` from the current block.

To get a <em>time weighted average tick</em> or <em>liquidity-in-range</em>, you must pass two time values: 
```
1) the beginning time 
2) the end time 
```
For example, to get the average tick for the last hour,
you should call it with `secondsAgos` = [3600, 0].

The time weighted average tick represents the geometric time weighted average price of the pool, in
log base sqrt(1.0001) of token1 / token0. The TickMath library can be used to go from a tick value to a ratio of the two tokens in the pool.

#### Parameters:

| Name          | Type     | Description                                                                   |
| :------------ | :------- | :---------------------------------------------------------------------------- |
| `secondsAgos` | uint32[] | From how long ago each cumulative tick and liquidity value should be returned |

#### Return Values:

| Name                                 | Type      | Description                                                                                     |
| :----------------------------------- | :-------- | :---------------------------------------------------------------------------------------------- |
| `tickCumulatives`                    | int56[]   | Cumulative tick values as of each `secondsAgos` from the current block timestamp                |
| `secondsPerLiquidityCumulativeX128s` | uint160[] | Cumulative seconds per liquidity-in-range value as of each `secondsAgos` from the current block |

timestamp

### increaseObservationLength

```solidity
  function increaseObservationLength(
    uint16 observationLengthNext
  ) external override lock noDelegateCall
```

Increase the maximum number of price and liquidity observations that can be stored by the pool.

This method will not modify state if the pool already has an observationLengthNext greater than or equal to
the input observationLengthNext.

#### Parameters:

| Name                         | Type   | Description                                                      |
| :--------------------------- | :----- | :--------------------------------------------------------------- |
| `observationLengthNext` | uint16 | The desired minimum number of observations for the pool to store |

### initialize

```solidity
  function initialize(
    uint160 sqrtPriceX96
  ) external override
```

Sets the initial price for the pool.

Initializes `unlocked`.

#### Parameters:

| Name           | Type    | Description                                    |
| :------------- | :------ | :--------------------------------------------- |
| `sqrtPrice64X96` | uint160 | the initial sqrt price of the pool as a Q64.96 |

### mint

```solidity
  function mint(
    address recipient,
    int24 tickLower,
    int24 tickUpper,
    uint128 amount,
    bytes data
  ) external override lock returns (uint256 amount0, uint256 amount1)
```

Adds liquidity for the given recipient.

`tickLower` will be the lower tick for the position.

`tickUpper` will be the upper tick for the position.

If the tick is outside of this range, this `Position` will not collect fees.

#### Parameters:

| Name        | Type    | Description                                              |
| :---------- | :------ | :------------------------------------------------------- |
| `recipient` | address | The address for which the liquidity will be created      |
| `tickLower` | int24   | The lower tick of the position in which to add liquidity |
| `tickUpper` | int24   | The upper tick of the position in which to add liquidity |
| `amount`    | uint128 | The amount of liquidity to mint                          |
| `data`      | bytes   | Any data that should be passed through to the callback   |

#### Return Values:

| Name      | Type    | Description                                                                                                 |
| :-------- | :------ | :---------------------------------------------------------------------------------------------------------- |
| `amount0` | uint256 | The amount of token0 that was paid to mint the given amount of liquidity. Matches the value in the callback |
| `amount1` | uint256 | The amount of token1 that was paid to mint the given amount of liquidity. Matches the value in the callback |

### collect

```solidity
  function collect(
    address recipient,
    int24 tickLower,
    int24 tickUpper,
    uint128 amount0Requested,
    uint128 amount1Requested
  ) external override lock returns (uint128 amount0, uint128 amount1)
```

Collects fees owed to a position.

Does not recompute fees earned, which must be done either via `mint` or `burn`.

Collect must be called by the `Position` NFT owner. To withdraw only token0 or only token1, `amount0Requested` or
`amount1Requested` may be set to zero. To withdraw all tokens owed, caller may pass any value greater than the
actual tokens owed, e.g. type(uint128).max. Tokens owed may be from accumulated swap fees or burned liquidity.

#### Parameters:

| Name               | Type    | Description                                              |
| :----------------- | :------ | :------------------------------------------------------- |
| `recipient`        | address | The address which should receive the fees collected      |
| `tickLower`        | int24   | The lower tick of the position for which to collect fees |
| `tickUpper`        | int24   | The upper tick of the position for which to collect fees |
| `amount0Requested` | uint128 | How much token0 should be withdrawn from the fees owed   |
| `amount1Requested` | uint128 | How much token1 should be withdrawn from the fees owed   |

#### Return Values:

| Name      | Type    | Description                            |
| :-------- | :------ | :------------------------------------- |
| `amount0` | uint128 | The amount of fees collected in token0 |
| `amount1` | uint128 | The amount of fees collected in token1 |

### burn

```solidity
  function burn(
    int24 tickLower,
    int24 tickUpper,
    uint128 amount
  ) external override lock returns (uint256 amount0, uint256 amount1)
```

Burn liquidity from the sender. `collect` must be called after `burn` to receive liquidity removed from the `Position` NFT.

noDelegateCall is applied indirectly via \_modifyPosition

#### Parameters:

| Name        | Type    | Description                                                |
| :---------- | :------ | :--------------------------------------------------------- |
| `tickLower` | int24   | The lower tick of the position for which to burn liquidity |
| `tickUpper` | int24   | The upper tick of the position for which to burn liquidity |
| `amount`    | uint128 | How much liquidity to burn                                 |

#### Return Values:

| Name      | Type    | Description                                |
| :-------- | :------ | :----------------------------------------- |
| `amount0` | uint256 | The amount of token0 sent to the recipient |
| `amount1` | uint256 | The amount of token1 sent to the recipient |

### swap

```solidity
  function swap(
    address recipient,
    bool zeroForOne,
    int256 amountSpecified,
    uint160 sqrtPriceLimitX96,
    bytes data
  ) external override noDelegateCall returns (int256 amount0, int256 amount1)
```

Swap token0 for token1, or token1 for token0

The caller of this method receives a callback in the form of IOceanbookV1SwapCallback. This will ensure that the user interacted with a genuine Oceanbook v1 pool.

#### Parameters:

| Name                | Type    | Description                                                                                                                                                                        |
| :------------------ | :------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `recipient`         | address | The address to receive the output of the swap                                                                                                                                      |
| `zeroForOne`        | bool    | The direction of the swap, true for token0 to token1, false for token1 to token0                                                                                                   |
| `amountSpecified`   | int256  | The amount of the swap, which implicitly configures the swap as exact input (positive), or exact output (negative)                                                                 |
| `sqrtPriceLimitX96` | uint160 | The Q64.96 sqrt price limit. If zero for one, the price cannot be less than this value after the swap. If one for zero, the price cannot be greater than this value after the swap |
| `data`              | bytes   | Any data to be passed through to the callback                                                                                                                                      |

#### Return Values:

| Name      | Type   | Description                                                                                |
| :-------- | :----- | :----------------------------------------------------------------------------------------- |
| `amount0` | int256 | The delta of the balance of token0 of the pool, exact when negative, minimum when positive |
| `amount1` | int256 | The delta of the balance of token1 of the pool, exact when negative, minimum when positive |

### flash

```solidity
  function flash(
    address recipient,
    uint256 amount0,
    uint256 amount1,
    bytes data
  ) external override lock noDelegateCall
```

Receive token0 and/or token1 and pay it back plus a fee of 0.1% (changeable by governance) in the callback.

The caller of this method receives a callback in the form of IPoolsharkV1FlashCallback.

[//]: # (Can be used to donate underlying tokens pro-rata to currently in-range liquidity providers by calling with 0 amount{0,1} and sending the donation amount(s) from the callback)

#### Parameters:

| Name        | Type    | Description                                                  |
| :---------- | :------ | :----------------------------------------------------------- |
| `recipient` | address | The address which will receive the token0 and token1 amounts |
| `amount0`   | uint256 | The amount of token0 to send                                 |
| `amount1`   | uint256 | The amount of token1 to send                                 |
| `data`      | bytes   | Any data to be passed through to the callback                |

### setFeeProtocol

```solidity
  function setFeeProtocol(
    uint8 feeProtocol0,
    uint8 feeProtocol1
  ) external override lock onlyFactoryOwner
```

Set the denominator of the protocol's % share of the fees

#### Parameters:

| Name           | Type  | Description                             |
| :------------- | :---- | :-------------------------------------- |
| `feeProtocol0` | uint8 | new protocol fee for token0 of the pool |
| `feeProtocol1` | uint8 | new protocol fee for token1 of the pool |

### collectProtocol

```solidity
  function collectProtocol(
    address recipient,
    uint128 amount0Requested,
    uint128 amount1Requested
  ) external override lock onlyFactoryOwner returns (uint128 amount0, uint128 amount1)
```

Collect the protocol fee accrued to the pool

#### Parameters:

| Name               | Type    | Description                                                                   |
| :----------------- | :------ | :---------------------------------------------------------------------------- |
| `recipient`        | address | The address to which collected protocol fees should be sent                   |
| `amount0Requested` | uint128 | The maximum amount of token0 to send, can be 0 to collect fees in only token1 |
| `amount1Requested` | uint128 | The maximum amount of token1 to send, can be 0 to collect fees in only token0 |

#### Return Values:

| Name      | Type    | Description                          |
| :-------- | :------ | :----------------------------------- |
| `amount0` | uint128 | The protocol fee collected in token0 |
| `amount1` | uint128 | The protocol fee collected in token1 |
