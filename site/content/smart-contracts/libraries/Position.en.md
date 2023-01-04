Position NFTs represent the owner's liquidity between a lower and upper tick boundary.

Positions store additional state for tracking fees owed to the position.

## Structs

### Info

```solidity
  struct Info {
        uint128 liquidity;
        uint256 feeGrowthInside0LastX128;
        uint256 feeGrowthInside1LastX128;
        uint128 tokensOwed0;
        uint128 tokensOwed1;
  }
```

#### Members:

| Name        | Type                                     | Description                               |
| :---------- | :--------------------------------------- | :---------------------------------------- |
| `liquidity`      | uint128 | the amount of liquidity owned by this position |
| `feeGrowthInside0LastX128`     | uint256                                  | The fee growth inside the tick range for token0 as of the last update to this position  |
| `feeGrowthInside1LastX128` | uint256                                    | The fee growth inside the tick range for token1 as of the last update to this position   |
| `tokensOwed0` | uint128                                    | the fees owed to the position owner in token0   |
| `tokensOwed1` | uint128                                    | the fees owed to the position owner in token1   |


## Functions

### get

```solidity
  function get(
    mapping(bytes32 => struct Position.Info) self,
    address owner,
    int24 tickLower,
    int24 tickUpper
  ) internal view returns (struct Position.Info position)
```

Returns the Info struct of a `Position`, given the owner and tick boundaries.

#### Parameters:

| Name        | Type                                     | Description                               |
| :---------- | :--------------------------------------- | :---------------------------------------- |
| `self`      | mapping(bytes32 => struct Position.Info) | The mapping containing all user positions |
| `owner`     | address                                  | The address of the position owner         |
| `tickLower` | int24                                    | The lower tick boundary of the position   |
| `tickUpper` | int24                                    | The upper tick boundary of the position   |

#### Return Values:

| Name       | Type                 | Description                                            |
| :--------- | :------------------- | :----------------------------------------------------- |
| `position` | struct Position.Info | The position info struct of the given owners' position |

### update

```solidity
  function update(
    struct Position.Info self,
    int128 liquidityDelta,
    uint256 feeGrowthInside0X128,
    uint256 feeGrowthInside1X128
  ) internal
```

Credits accumulated fees to a user's position

#### Parameters:

| Name                   | Type                 | Description                                                                                     |
| :--------------------- | :------------------- | :---------------------------------------------------------------------------------------------- |
| `self`                 | struct Position.Info | The mapping containing all user positions                                                       |
| `liquidityDelta`       | int128               | The change in pool liquidity as a result of the position update                                 |
| `feeGrowthInside0X128` | uint256              | The all-time fee growth in token0, per unit of liquidity, inside the position's tick boundaries |
| `feeGrowthInside1X128` | uint256              | The all-time fee growth in token1, per unit of liquidity, inside the position's tick boundaries |
