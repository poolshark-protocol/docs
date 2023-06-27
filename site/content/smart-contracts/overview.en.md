
Poolshark is a set of smart contracts comprised of support for range liquidity, cover liquidity, and price liquidity.

The smart contract's base purpose is to provide fundamental guarantees for all interfacing parties. They define the logic of permissionlessly creating new pools, adding liquidity, executing swaps, accumulating across ticks, etc.

---

## Cover Pools
> [**Cover Factory Reference**](./cover/CoverPoolFactory.en.md)

The factory defines the logic for generating `Cover Pools`. A pool is defined by two tokens and a volatility tier. Multiple pools of the same pair can exist, distinguished by the input pool being tracked as well as the auction parameters (i.e. `tickSpread`, `twapLength`, and `auctionLength`).

> [**Cover Pool Reference**](./cover/CoverPool.en.md)

Cover Pools allow liquidity providers to increase exposure when token price is increasing and decrease exposure when token price is decreasing.

> [**Cover Solidity Contracts**](https://github.com/poolsharks-protocol/cover)

---

## Limit Pools

> [**Limit Factory Reference**](./limit/LimitPoolFactory.en.md)

The factory defines the logic for generating `Limit Pools`. A pool is defined by two tokens. `Limit Pools` differ from `Range Pools` in that LP positions only trade in one direction.

> [**Limit Pool Reference**](./limit/LimitPool.en.md)

`Limit Pools` allow liquidity providers to decrease exposure when token price is increasing.

> **Limit Solidity Contracts** (open-source soon)
<br/>
---

## Range Pools

> [**Range Factory Reference**](./range/RangePoolFactory.en.md)

The factory defines the logic for generating `Range Pools`. A range pool is defined by two tokens, which make up the asset pair, and a fee tier. Multiple pools of the same pair can exist, distinguished by each fee tier in existence.

> [**Range Pool Reference**](./range/RangePool.en.md)

Range Pools allow liquidity providers to have fungible two-way liquidity and autocompounding.

> [**Samples Reference**](./libraries/Samples.en.md)

The `Samples` library allows for on-chain price and liquidity oracle data to be aggregated for a wide variety of use cases both on-chain and off-chain.  is turned off by default in all `Range Pools` and is automatically expanded via `Cover Pools` as needed.

> [**Range Solidity Contracts**](https://github.com/poolsharks-protocol/range)

---

<br/><br/><br/><br/>