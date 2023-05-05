Creates and gets cover pools. 

## Functions

### createCoverPool

```solidity
    function createCoverPool(
        bytes32 sourceName,
        address tokenIn,
        address tokenOut,
        uint16 feeTier,
        int16  tickSpread,
        uint16 twapLength
    ) external override returns (address pool)
```
Creates a pool for the given two ERC-20 tokens to correspond with an existing volatility tier.

The volatility tier selected is based on the `sourceName`, `feeTier`, `tickSpread`, and `twapLength` passed in.

The addresses of `tokenIn` and `tokenOut` will have their addresses sorted lexographically (i.e. first by number then by letter) to represent `token0` and `token1`.

The contract call will revert with `PoolAlreadyExists()` if the pool already exists, `TwapSourceNotFound` is the TWAP source does not exists, `VolatilityTierNotSupported()` if the volatility tier is not supported, or `InvalidTokenAddress` if one of the token addresses is invalid.

** Parameters: **

| Name     | Type    | Description                                     |
| :------- | :------ | :---------------------------------------------- |
| `sourceName` | bytes32 | A bytes string with the name of the TWAP source being used (e.g. 'UNI-V3')     |
| `tokenIn` | address | The first ERC-20 token by ordering in the pool     |
| `tokenOut` | address | The second ERC-20 token by ordering in the pool |
| `feeTier`      | uint16  | The selected fee tier from which to derive TWAP data                    |
| `tickSpread`| int16 | The spacing for the ticks which will create a spread around the TWAP |
| `twapLength`| uint16 | The length in seconds for the TWAP sample which matches a volatility tier |

** Return Values: **

| Name   | Type    | Description                           |
| :----- | :------ | :------------------------------------ |
| `pool` | address | The generated address for the pool    |

### getCoverPool

```solidity
    function getCoverPool(
        bytes32 sourceName,
        address tokenIn,
        address tokenOut,
        uint16 feeTier,
        int16  tickSpread,
        uint16 twapLength
    ) external view override returns (address)
```

Gets the pool for the given two ERC-20 tokens with the selected fee tier.

If such a pool does not exist, `address(0)` will be returned.

** Parameters: **

| Name     | Type    | Description                                     |
| :------- | :------ | :---------------------------------------------- |
| `sourceName` | bytes32 | A bytes string with the name of the TWAP source being used (e.g. 'UNI-V3')     |
| `tokenIn` | address | The first ERC-20 token by ordering in the pool     |
| `tokenOut` | address | The second ERC-20 token by ordering in the pool |
| `feeTier`      | uint16  | The selected fee tier from which to derive TWAP data                    |
| `tickSpread`| int16 | The spacing for the ticks which will create a spread around the TWAP |
| `twapLength`| uint16 | The length in seconds for the TWAP sample which matches a volatility tier |

** Return Values: **

| Name   | Type    | Description                           |
| :----- | :------ | :------------------------------------ |
| `pool` | address | The address of the found pool (if exists)    |

<br/><br/>
<br/><br/>