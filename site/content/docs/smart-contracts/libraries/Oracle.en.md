
The `Oracle` library provides average tick (i.e. price) and liquidity data that can be utilized for on-chain and off-chain consumption. An array of oracle data titled `observations` is kept in contract storage and is publicly available for read.

Each entry in the oracle array contains averages across a single block of transactions. Each contract starts with an oracle array length of 1. Anyone can [increase the number of historical observations](https://docs.poolsharks.org/smart-contracts/base/PoolsharkPair#increaseobservationlengthnext).

When all indices in the oracle array are full, the index will reset to `0`. The most recent observation is available by passing in `0` to `observe()`.

## Functions

### initialize

```solidity
  function initialize(
    struct Oracle.Observation[65535] self,
    uint32 time
  ) internal returns (uint16 length, uint16 lengthNext)
```

Writes the first index of the oracle array. Callable only once.

#### Parameters:

| Name   | Type                             | Description                                                                    |
| :----- | :------------------------------- | :----------------------------------------------------------------------------- |
| `self` | struct Oracle.Observation[65535] | The stored oracle array                                                        |
| `time` | uint32                           | The time of the initialization, i.e. block.timestamp cast as a uint32 |

#### Return Values:

| Name              | Type   | Description                                                   |
| :---------------- | :----- | :------------------------------------------------------------ |
| `length`     | uint16 | The number of elements which have oracle data |
| `lengthNext` | uint16 | The new length of the oracle array                    |

### write

```solidity
  function write(
    struct Oracle.Observation[65535] self,
    uint16 index,
    uint32 blockTimestamp,
    int24 tick,
    uint128 liquidity,
    uint16 length,
    uint16 lengthNext
  ) internal returns (uint16 indexUpdated, uint16 lengthUpdated)
```

Writes an `Observation` to the `observations` array.

Can be called at most once per block. `index` represents the most recently written element. `length` and `index` must be tracked externally.

The oracle array length will only be increased when `index` is at the end of the allowable array length and `lengthNext` is greater than `index`. This preserves ordering.

#### Parameters:

| Name              | Type                             | Description                                                     |
| :---------------- | :------------------------------- | :-------------------------------------------------------------- |
| `self`            | struct Oracle.Observation[65535] | The stored oracle array                                         |
| `index`           | uint16                           | The location of the most recently updated observation           |
| `blockTimestamp`  | uint32                           | The timestamp of the new observation                            |
| `tick`            | int24                            | The active tick at the time of the new observation              |
| `liquidity`       | uint128                          | The total in-range liquidity at the time of the new observation |
| `length`     | uint16                           | The number of populated elements in the oracle array            |
| `lengthNext` | uint16                           | The new length of the oracle array, independent of population   |

#### Return Values:

| Name                 | Type   | Description                                                            |
| :------------------- | :----- | :--------------------------------------------------------------------- |
| `indexUpdated`       | uint16 | The index of the most recently written entry in the oracle array |
| `lengthUpdated` | uint16 | The new length of the oracle array                                |

### grow

```solidity
  function grow(
    struct Oracle.Observation[65535] self,
    uint16 current,
    uint16 next
  ) internal returns (uint16)
```

Prepares the oracle array to store up to `next` observations.

#### Parameters:

| Name      | Type                             | Description                                                               |
| :-------- | :------------------------------- | :------------------------------------------------------------------------ |
| `self`    | struct Oracle.Observation[65535] | The stored oracle array                                                   |
| `current` | uint16                           | The current next length of the oracle array                          |
| `next`    | uint16                           | The proposed next length which will be populated in the oracle array |

#### Return Values:

| Name   | Type   | Description                                                      |
| :----- | :----- | :--------------------------------------------------------------- |
| `next` | uint16 | The next length which will be populated in the oracle array |

### observe

```solidity
  function observe(
    struct Oracle.Observation[65535] self,
    uint32 time,
    uint32[] secondsAgos,
    int24 tick,
    uint16 index,
    uint128 liquidity,
    uint16 length
  ) internal view returns (int56[] tickCumulatives, uint160[] liquidityCumulatives)
```

Returns the cumulative tick and liquidity values as of each time in the array `secondsAgos`.

Reverts if `secondsAgos` > oldest observation.

#### Parameters:

| Name          | Type                             | Description                                                                           |
| :------------ | :------------------------------- | :------------------------------------------------------------------------------------ |
| `self`        | struct Oracle.Observation[65535] | The stored oracle array                                                               |
| `time`        | uint32                           | The current block.timestamp                                                           |
| `secondsAgos` | uint32[]                         | Each amount of time to look back, in seconds, at which point to return an observation |
| `tick`        | int24                            | The current tick                                                                      |
| `index`       | uint16                           | The location of a given observation within the oracle array                           |
| `liquidity`   | uint128                          | The current in-range pool liquidity                                                   |
| `length` | uint16                           | The number of populated elements in the oracle array                                  |

#### Return Values:

| Name                   | Type      | Description                                                                                 |
| :--------------------- | :-------- | :------------------------------------------------------------------------------------------ |
| `tickCumulatives`      | int56[]   | The tick \* time elapsed since the pool was first initialized, as of each `secondsAgo`      |
| `liquidityCumulatives` | uint160[] | The liquidity \* time elapsed since the pool was first initialized, as of each `secondsAgo` |
