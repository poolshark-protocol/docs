Launches OceanBook v1 pools and managers ownership controls as well as fee accrual if enabled. 

## Functions

### createPool

```solidity
  function createPool(
    address token20A,
    address token20B,
    uint24 fee
  ) external returns (address pool)
```

Creates a pool for the given two ERC-20 tokens and fee tier.

The addresses of `token20A` and `token20B` will be sorted lexographically (i.e. first by number then by letter) based on their addresses.

This will correspond to `token0` and `token1` in the pool created. 

`tickSpacing` is retrieved based on the fee tier selected. The contract call will revert if the pool already exists, the fee tier is not supported, or the token addresses are invalid.

** Parameters: **

| Name     | Type    | Description                                     |
| :------- | :------ | :---------------------------------------------- |
| `token20A` | address | The first ERC-20 token to pair in the pool       |
| `token20B` | address | The second ERC-20 token to pair in the pool |
| `fee`    | uint24  | The selected fee tier for the pool                    |

** Return Values: **

| Name   | Type    | Description                           |
| :----- | :------ | :------------------------------------ |
| `pool` | address | The generated address for the token pool |

### setOwner

```solidity
  function setOwner(
    address _owner
  ) external
```

Sets the owner of the factory contract.

The `owner` is set to `msg.sender` when the factory contract is first launched.

Admin functions:
`setOwner`
`enableFeeTier`

** Parameters: **

| Name     | Type    | Description                  |
| :------- | :------ | :--------------------------- |
| `_owner` | address | The new owner of the factory |

### enableFeeTier

```solidity
  function enableFeeTier(
    uint24 fee,
    int24 tickSpacing
  ) public
```

Enables a fee tier with the selected tickSpacing.

Fee amounts can never be removed by anyone once enabled.

** Parameters: **

| Name          | Type   | Description                                                                              |
| :------------ | :----- | :--------------------------------------------------------------------------------------- |
| `fee`         | uint24 | The fee amount to enable, denominated in hundredths of a basis points (i.e. 0.0001%)                 |
| `tickSpacing` | int24  | The spacing between ticks to be enforced for all pools created with the given fee amount denoted in basis points (i.e. 0.01%) |

<br/><br/>
<br/><br/>