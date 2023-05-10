Creates and gets range pools. 

## Functions

### createRangePool

```solidity
  function createRangePool(
      address tokenIn,
      address tokenOut,
      uint16  swapFee,
      uint160 startPrice
  ) external override returns (address pool)
```

Creates a pool for the given two ERC-20 tokens with the selected fee tier.

The addresses of `tokenIn` and `tokenOut` will have their addresses sorted lexographically (i.e. first by number then by letter) to represent `token0` and `token1`.

`tickSpacing` is retrieved based on the fee tier selected. 

The contract call will revert with `PoolAlreadyExists()` if the pool already exists, `FeeTierNotSupported()` if the fee tier is not supported, or `InvalidTokenAddress` if one of the token addresses is invalid.

** Parameters: **

| Name     | Type    | Description                                     |
| :------- | :------ | :---------------------------------------------- |
| `tokenIn` | address | The first ERC-20 token by ordering in the pool     |
| `tokenOut` | address | The second ERC-20 token by ordering in the pool |
| `swapFee`      | uint24  | The selected fee tier for the pool                    |
| `startPrice`| uint256 | The select maker tier defining the minimum order size |

** Return Values: **

| Name   | Type    | Description                           |
| :----- | :------ | :------------------------------------ |
| `pool` | address | The generated address for the pool    |

### getRangePool

```solidity
  function getRangePool(
      address tokenIn,
      address tokenOut,
      uint256 swapFee
  ) public view override returns (address)
```

Gets the pool for the given two ERC-20 tokens with the selected fee tier.

If such a pool does not exist, `address(0)` will be returned.

** Parameters: **

| Name     | Type    | Description                                     |
| :------- | :------ | :---------------------------------------------- |
| `tokenIn` | address | The first ERC-20 token to pair in the pool      |
| `tokenOut` | address | The second ERC-20 token to pair in the pool |
| `swapFee`      | uint24  | The selected fee tier for the po                    |

** Return Values: **

| Name   | Type    | Description                           |
| :----- | :------ | :------------------------------------ |
| `pool` | address | The address of the found pool (if exists)    |

<br/><br/>
<br/><br/>