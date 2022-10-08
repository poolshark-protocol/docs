Launches OceanBook v1 queues, manages ownership controls, fee accrual, and maker size. 

## Functions

### createBook

```solidity
  function createQueue(
    address token20A,
    address token20B,
    uint24 feeTier,
    uint256 makerTier
  ) external returns (address pool)
```

Creates a queue for the given two ERC-20 tokens and fee tier.

A queue differs from a pool in that liquidity is not reused like in a pool.

Queues do not support pro-rata fills, meaning the fees will go to liquidity providers based on price-time priority.

The addresses of `token20A` and `token20B` will be sorted lexographically (i.e. first by number then by letter) based on their addresses.

This will correspond to `token0` and `token1` in the queue created. 

`tickSpacing` is retrieved based on the fee tier selected. The contract call will revert if the queue already exists, the fee or maker tier is not supported, or the token addresses are invalid.

#### Parameters:

| Name     | Type    | Description                                     |
| :------- | :------ | :---------------------------------------------- |
| `token20A` | address | The first ERC-20 token to pair in the queue      |
| `token20B` | address | The second ERC-20 token to pair in the queue |
| `feeTier`      | uint24  | The selected fee tier for the queue                    |
| `makerTier`| uint256 | The select maker tier defining the minimum order size |

#### Return Values:

| Name   | Type    | Description                           |
| :----- | :------ | :------------------------------------ |
| `queue` | address | The generated address for the token queue |

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

#### Parameters:

| Name     | Type    | Description                  |
| :------- | :------ | :--------------------------- |
| `_owner` | address | The new owner of the factory |

### enableFeeTier

```solidity
  function enableFeeTier(
    uint24 feeTier,
    int24 tickSpacing
  ) public
```

Enables a fee tier with the selected tickSpacing and makerSize.

Fee amounts can never be removed by anyone once enabled.

#### Parameters:

| Name          | Type   | Description                                                                              |
| :------------ | :----- | :--------------------------------------------------------------------------------------- |
| `feeTier`     | uint24 | The fee amount to enable, denominated in hundredths of a basis points (i.e. 0.0001%)                 |
| `tickSpacing` | int24  | The spacing between ticks to be enforced for all books created with the given fee amount denoted in basis points (i.e. 0.01%) |

### enableMakerTier

```solidity
  function enableFeeTier(
    uint24 feeTier,
    uint256 makerTier
  ) public
```

Enables a maker tier with the selected tick spacing and fee tier.

Maker tiers exist to provide deterministic gas costs for liquidity takers. This prevents makers from keeping the price artificially low with tiny amounts of liquidity.

Maker tiers can never be removed by anyone once enabled.

#### Parameters:

| Name          | Type   | Description                                                                              |
| :------------ | :----- | :--------------------------------------------------------------------------------------- |
| `feeTier`     | uint24 | The fee amount to enable, denominated in hundredths of a basis points (i.e. 0.0001%)                 |
| `makerTier`   | uint256| The minimum order size for which smaller orders will be rejected to maintain deterministic gas costs for the taker |

<br/><br/>
<br/><br/>