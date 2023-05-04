
Poolshark is a set of smart contracts comprised of support for range liquidity, cover liquidity, and price liquidity.

The smart contracts' goal is to provide fundamental guarantees for liquidity providers and traders. They define the logic of permissionlessly creating new pools, adding and removing liquidity, executing swaps, etc.

### Range Pools

> [**Poolshark Range Source Code**](https://github.com/poolsharks-protocol/range)

Range Pools allow liquidity providers to have fungible two-way liquidity and autocompounding.

### Cover Pools

> [**Cover Pool Source Code**] (open-source soon)

Cover Pools allow liquidity providers to increase exposure when token price is increasing.

### Price Pools

> [**Price Pool Reference**] (open-source soon)

Price Pools allow liquidity providers to decrease exposure when token price is increasing.

### Factory

> [**Range Factory Reference**](../base/RangePoolFactory)

The factory defines the logic for creating and getting `Range Pools`. A range pool is defined by two tokens and a fee tier. Multiple pools of the same pair can exist with different fee tiers.

> [**Cover Factory Reference**](../base/CoverPoolFactory)

The factory defines the logic for generating `Cover Pools`. A pool is defined by two tokens and a volatility tier. Multiple pools of the same pair can exist, distinguished by the input pool being tracked as well as the auction parameters (i.e. `tickSpread`, `twapLength`, and `auctionLength`).

> [**Price Factory Reference**](../base/PricePoolFactory)

The factory defines the logic for generating `Price Pools`. A pool is defined by two tokens. `Price Pools` differ from `Range Pools` in that LP positions only trade in one direction.

### Oracle

> [**Samples Reference**](./libraries/Samples.en.md)

The `Samples` library allows for on-chain price and liquidity oracle data to be aggregated for a wide variety of use cases both on-chain and off-chain.  is turned off by default in all `Range Pools` and is automatically expanded via `Cover Pools` as needed.

<br/><br/><br/><br/>