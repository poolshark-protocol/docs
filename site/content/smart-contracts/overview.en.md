
Poolshark is a set of smart contracts comprised of support for range liquidity, cover liquidity, and price liquidity.

The smart contract's base purpose is to provide fundamental guarantees for all interfacing parties. They define the logic of permissionlessly creating new pools, adding liquidity, executing swaps, accumulating across ticks, etc.

## Base

> **Poolshark Source Code** (January 2023 release)

The base consists of a factory contract, a router, and the pool contract being launched by the factory.

The contracts have been gas optimized in both the Sway and Solidity versions respectively with attention given to code clarity to maximize the developer integration experience.

### Factory

> [**Range Factory Reference**](./range/RangePoolFactory)

The factory defines the logic for generating `Range Pools`. A range pool is defined by two tokens, which make up the asset pair, and a fee tier. Multiple pools of the same pair can exist, distinguished by each fee tier in existence.

> [**Cover Factory Reference**](../cover/CoverPoolFactory)

The factory defines the logic for generating `Cover Pools`. A pool is defined by two tokens, which make up the asset pair, and a fee tier. `Cover Pools` differ from `Range pools` in that LP positions only trade in one direction. Multiple pools of the same pair can exist, distinguished by fee tier, input pool, as well as the auction parameters (i.e. `scaleFactor`, `decayConstant`, and `tickSpread`).

> [**Limit Factory Reference**](../limit/LimitPoolFactory)

The factory defines the logic for generating `Limit Pools`. A book is defined by two tokens, which make up the asset pair, and a fee tier. `Limit Pools` differ from `Range pools` in that LP positions only trade in one direction. Multiple price pools of the same pair can exist, distinguished by each fee tier.

### Range Pools

> [**Poolshark Range Source Code**](https://github.com/poolsharks-protocol/range)

Range Pools allow liquidity providers to have fungible two-way liquidity and autocompounding.

### Cover Pools

> [**Cover Pool Source Code**] (open-source soon)

Cover Pools allow liquidity providers to increase exposure when token price is increasing.

### Limit Pools

> [**Limit Pool Reference**] (open-source soon)

Limit Pools allow liquidity providers to decrease exposure when token price is increasing.

### Factory

> [**Range Factory Reference**](../base/RangePoolFactory)

The factory defines the logic for creating and getting `Range Pools`. A range pool is defined by two tokens and a fee tier. Multiple pools of the same pair can exist with different fee tiers.

> [**Cover Factory Reference**](../base/CoverPoolFactory)

The factory defines the logic for generating `Cover Pools`. A pool is defined by two tokens and a volatility tier. Multiple pools of the same pair can exist, distinguished by the input pool being tracked as well as the auction parameters (i.e. `tickSpread`, `twapLength`, and `auctionLength`).

> [**Limit Factory Reference**](../base/LimitPoolFactory)

The factory defines the logic for generating `Limit Pools`. A pool is defined by two tokens. `Limit Pools` differ from `Range Pools` in that LP positions only trade in one direction.

### Oracle

> [**Samples Reference**](./libraries/Samples.en.md)

The `Samples` library allows for on-chain price and liquidity oracle data to be aggregated for a wide variety of use cases both on-chain and off-chain.  is turned off by default in all `Range Pools` and is automatically expanded via `Cover Pools` as needed.

<br/><br/><br/><br/>