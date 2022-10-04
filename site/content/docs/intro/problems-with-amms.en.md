# Problems With AMMs

># **Slippage On Constant Function Market Makers**

For traders exchange tokens on CFMMs (e.g. Uniswap v3), they are often subject to increasing slippage on larger trades.

This `slippage` is derived on the variance in the token reserves and is ultimately a passive pricing model to predict what price the liquidity provider should exchange at.

![Screenshot](slippage.jpeg){: .center style=""}

When this slippage exceeds the price on another liquidity source (e.g. a centralized exchange), arbitrageurs
will bring the price on the AMM pool up to par.

What this demonstrates is that passive pricing from Automated Market Makers cannot surpass the efficiency of active pricing from a Central Limit Order Book. The scalability issues of the blockchain are what prevent this limitation from being surpassed.

The OceanBook Protocol enables market makers to undercut the current market price and receive fees accordingly.

This can happen in namely two ways
```
1. Directional LPing
2. Priority Queueing
```

Using either of these methods will result in the ability to offer lower prices than the traditional Liquidity Pools.

The outcome is better for the Liquidity Provider in those scenarios if the following are true:
```
1. Directional LPing
2. Priority Queueing
```

Any liquidity that is added to the Priority Queue (skip to section) will result in 0% slippage for traders. The positive tradeoff for the Market Maker is they receive 100% of fees for liquidity provided.