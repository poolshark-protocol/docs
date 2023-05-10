Manages cover liquidity positions.

## Functions

### mint

```solidity
    function mint(
        MintParams memory params
    ) external lock

    struct MintParams {
            address to;
            uint128 amount;
            int24 lower;
            int24 claim;
            int24 upper;
            bool zeroForOne;
    }
```
Mints a Cover LP for the range `lower` to `upper`.

`lower` will be the lower price tick for the position.

`upper` will be the upper tick for the position.

Both `lower` and `upper` must be multiples of the `tickSpread` for the pool.

`claim` only need be an exact value in the case the user has already minted a position with the same `lower` and `upper`.

If this is the case, the `claim` tick must be the furthest tick crossed into the position.

`zeroForOne` as `true` means the LP deposits `token0` and is filled with `token1`. `zeroForOne` as `false` means the LP deposits `token1` and is filled with `token0`.

** Parameters: **

| Name        | Type  | Description                 |
| :---------- | :---- | :-------------------------- |
| `to` | int24 | The recipient of the fungible position |
| `lower` | int24 | The lower price tick of the range |
| `claim` | int24 | The claim price tick of the range |
| `upper` | int24 | The upper price tick of the range |
| `amount` | uint128 | The amount of the input token to add to the `Position` |
| `zeroForOne` | bool | `true` for `token0` => `token1` and `false` for `token1` => `token0` |

** Return Values: **

| Name      | Type    | Description                                                                                                 |
| :-------- | :------ | :---------------------------------------------------------------------------------------------------------- |
| `amount` | uint256 | The amount of the input token that was added to mint liquidity. |

### burn

```solidity
    function burn(
        BurnParams memory params
    ) external lock

    struct BurnParams {
            address to;
            uint128 burnPercent;
            int24 lower;
            int24 claim;
            int24 upper;
            bool zeroForOne;
            bool sync;
    }
```

Burns liquidity from `msg.sender`. The token received from the burned liquidity is then sent to the address `to`.

`burnPercent` is a number no greater than `1e38` which equals 100%.

`lower` and `upper` must match a position owned by the caller.

`zeroForOne` will be `true` if the LP is trading `token1` for `token0` and `false` if the LP is trading `token1` for `token0`.

`sync` should be `true` in most cases to receive the `syncFee` if available. `false` should only be used if the user wants to exit their LP without syncing the pool.

** Parameters: **

| Name        | Type    | Description                                                |
| :---------- | :------ | :--------------------------------------------------------- |
| `to` | int24   | The recipient of the token from the burned liquidity |
| `burnPercent` | uint128 | The percent of the user's liquidity to be burned and collected (1e38 = 100%) |
| `lower` | int24 | The lower price tick of the range |
| `claim` | int24 | The claim price tick of the range |
| `upper` | int24 | The upper price tick of the range |
| `zeroForOne` | bool | `true` for `token0` => `token1` and `false` for `token1` => `token0` |
| `zeroForOne` | bool | `true` to allow sync and `false` to skip sync |


** Return Values: **

| Name      | Type    | Description                                                                                                 |
| :-------- | :------ | :---------------------------------------------------------------------------------------------------------- |
| `amount0` | uint256 | The amount of token0 collected for burning liquidity. Matches the value in the callback |
| `amount1` | uint256 | The amount of token1 collected for burning liquidity. Matches the value in the callback |

### swap

```solidity
    function swap(
        address recipient,
        bool zeroForOne,
        uint256 amountIn,
        uint160 priceLimit
    ) external override lock
```

Swaps `token0` for `token1` or `token1` for `token0`.

** Parameters: **

| Name                | Type    | Description                                                                                                                                                                        |
| :------------------ | :------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `recipient`         | address | The address to receive the output of the swap                                                                                                                                      |
| `zeroForOne`        | bool    | The direction of the swap, true for `token0` => `token1`, false for `token1` => `token0`                                                                                                   |
| `amountIn`   | int256  | The token amount for the swap                                                              |
| `priceLimit` | uint160 | The Q64.96 sqrt price limit. If `zeroForOne` is true, the price cannot be less than this value after the swap. If `zeroForOne` is false, the price cannot be greater than this value after the swap. |
| `data`              | bytes   | Raw data being passed through to the callback                                                                                                                                      |

### quote

```solidity
    function quote(
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
| `amountIn`   | int256  | The token amount for the swap                                                              |
| `priceLimit` | uint160 | The Q64.96 sqrt price limit. If `zeroForOne` is true, the price cannot be less than this value after the swap. If `zeroForOne` is false, the price cannot be greater than this value after the swap. |
| `data`              | bytes   | Raw data being passed through to the callback                                                                                                                                      |

** Return Values: **

| Name      | Type   | Description                                                                                |
| :-------- | :----- | :----------------------------------------------------------------------------------------- |
| `amount0` | uint128 | The change in the pool `token0` balance |
| `amount1` | uint128 | The change in the pool `token1` balance |


### collectProtocolFees

```solidity
    function protocolFees(
        uint16 syncFee,
        uint16 fillFee,
        bool setFees
    ) external ownerOnly returns (
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