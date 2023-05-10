Creates and gets price pools. 

## Functions

### createLimitPool

```solidity
    function createLimitPool(
        address tokenIn,
        address tokenOut
    ) external override returns (address pool)
```
Creates a Limit Pool for the given two ERC-20 tokens.

The addresses of `tokenIn` and `tokenOut` will have their addresses sorted lexographically (i.e. first by number then by letter) to represent `token0` and `token1`.

The contract call will revert with `PoolAlreadyExists()` if the pool already exists.

** Parameters: **

| Name     | Type    | Description                                     |
| :------- | :------ | :---------------------------------------------- |
| `tokenIn` | address | The first ERC-20 token by ordering in the pool     |
| `tokenOut` | address | The second ERC-20 token by ordering in the pool |

** Return Values: **

| Name   | Type    | Description                           |
| :----- | :------ | :------------------------------------ |
| `pool` | address | The generated address for the pool    |

### getLimitPool

```solidity
    function getLimitPool(
        address tokenIn,
        address tokenOut
    ) external view override returns (address)
```

Gets the pool for the given two ERC-20 tokens with the selected fee tier.

If such a pool does not exist, `address(0)` will be returned.

** Parameters: **

| Name     | Type    | Description                                     |
| :------- | :------ | :---------------------------------------------- |
| `tokenIn` | address | The first ERC-20 token by ordering in the pool     |
| `tokenOut` | address | The second ERC-20 token by ordering in the pool |

** Return Values: **

| Name   | Type    | Description                           |
| :----- | :------ | :------------------------------------ |
| `pool` | address | The address of the found pool (if exists)    |

<br/><br/>
<br/><br/>