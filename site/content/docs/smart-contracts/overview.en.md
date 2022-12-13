
Poolshark is a set of smart contracts comprised of support for concentrated liquidity, directional liquidity, and priority queues.

The smart contract's base job is to provide fundamental guarantees for all relevant entities. They define the logic of permissionlessly creating new pools, adding liquidity, executing swaps, etc.

## Base

> **Poolshark Source Code** (January 2023 release)

The base consists of a factory contract, a router, and the book contract which will be launched by the factory.

The contracts have been gas optimized in both the Sway and Solidity versions respectively with attention given to code clarity to maximize the developer integration experience.

### Factory

> [**Pool Factory Reference**](base/PoolsharkPairFactory.en.md)

The factory defines the logic for generating pools. A pool is defined by two tokens, which make up the asset pair, and a fee tier. Multiple pools of the same pair can exist, distinguished
by each fee tier in existence.

> [**Book Factory Reference**](base/PoolsharkBookFactory.en.md)

The factory defines the logic for generating books. A book is defined by two tokens, which make up the asset pair, and a fee tier. Books differ from pools in that LP positions only trade in one direction. Multiple book of the same pair can exist, distinguished by each fee tier and maker tier in existence.

### Pools

> [**Pool Reference**](base/PoolsharkPair.en.md).

Pools serve as both automated makers for the paired assets, expose price oracle data, and allow for flash swaps.

### Books

> [**Book Reference**](base/PoolsharkBook.en.md).

Books contain both automated and queued market makers for the paired assets. Additionally, expose price oracle data, and allow for flash swaps.

### Oracle

> [**Oracle Reference**](libraries/Oracle.en.md)

The oracle library allows for price and liquidity data to be aggregated for a wide variety of use cases both on-chain and off-chain. This oracle data is turned on by default in all books and pools.

<br/><br/><br/><br/>