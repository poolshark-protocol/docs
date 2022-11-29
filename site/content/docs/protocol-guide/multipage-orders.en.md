# MultiPage Orders

A `MultiPage Order` represents an order that will be filled by aggregating liquidity from several ticks of the available liquidity on `Poolshark`. In other terms, a tick can be considered to be a specific current price point for a given asset, and by aggregating several ticks worth of liquidity slippage can be reduced significantly, being that the average rounded current price will fluctuate less than in single-page orders. This is possible due to the use of several `Concentrated Liquidity` ranges from different LPs and by taking into account previous ticks (or pricepoints) from all liquidity sources and not just the current one. 

### MultiPage vs SinglePage

While `SinglePage Orders` only take into account a single current price reference for ticks, `MultiPage Orders` also make use of references from several different ticks in different concentrated liquidity ranges for a given asset, with the goal of reducing eventual slippage for a given swap.

<br/>
<br/>
<br/>