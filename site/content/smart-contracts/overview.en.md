
Poolshark is a set of smart contracts comprised of support for range liquidity, cover liquidity, and price liquidity.

The smart contract's base purpose is to provide fundamental guarantees for all interfacing parties. They define the logic of permissionlessly creating new pools, adding liquidity, executing swaps, accumulating across ticks, etc.

## Base

> **Poolshark Source Code** (January 2023 release)

The base consists of a factory contract, a router, and the pool contract being launched by the factory.

The contracts have been gas optimized in both the Sway and Solidity versions respectively with attention given to code clarity to maximize the developer integration experience.

### Factory

> [**Range Factory Reference**](base/PoolsharkRangeFactory)

The factory defines the logic for generating `Range Pools`. A range pool is defined by two tokens, which make up the asset pair, and a fee tier. Multiple pools of the same pair can exist, distinguished by each fee tier in existence.

> [**Cover Factory Reference**](base/PoolsharkCoverFactory)

The factory defines the logic for generating `Cover Pools`. A pool is defined by two tokens, which make up the asset pair, and a fee tier. `Cover Pools` differ from `Range pools` in that LP positions only trade in one direction. Multiple pools of the same pair can exist, distinguished by fee tier, input pool, as well as the auction parameters (i.e. `scaleFactor`, `decayConstant`, and `tickSpread`).

> [**Price Factory Reference**](base/PoolsharkPriceFactory)

The factory defines the logic for generating `Price Pools`. A book is defined by two tokens, which make up the asset pair, and a fee tier. `Price Pools` differ from `Range pools` in that LP positions only trade in one direction. Multiple price pools of the same pair can exist, distinguished by each fee tier.

### Range Pools

> [**Range Pool Reference**](base/PoolsharkRangePair).

Pools serve as both automated makers for the paired assets, expose price oracle data, and allow for flash swaps.

### Cover Pools

> [**Cover Pool Reference**](base/PoolsharkCoverPair).

Books contain both automated and queued market makers for the paired assets. Additionally, expose price oracle data, and allow for flash swaps.

### Price Pools

> [**Price Pool Reference**](base/PoolsharkPricePair).

Books contain both automated and queued market makers for the paired assets. Additionally, expose price oracle data, and allow for flash swaps.

### Oracle

> [**Oracle Reference**](libraries/Oracle.en.md)

The oracle library allows for price and liquidity data to be aggregated for a wide variety of use cases both on-chain and off-chain. This oracle data is turned off by default in all `Range Pools`.

<br/><br/><br/><br/>