# Concentrated Liquidity

### <em>What is Concentrated Liquidity?</em>

![Screenshot](concentrated-liquidity.png){: .center style="height:300px; width:400px;"}

`Concentrated Liquidity` is the ability given to `Liquidity Providers` to select a specific range in a given price curve to provide liquidity.

### <em>What is the main goal of using it?</em>

It serves as a solution to boost capital efficiency, making up for the limitations of the original `x*y=k` `AMM` model. In a `Concentrated Liquidity` model, `Liquidity Providers` don't have limitations on the number of positions open in a given pool and as such they are able to create unique price curves that are aligned with their current view of the market by setting `Range Orders` which will result in `Concentrated Liquidity Positions` that cover a particular liquidity range when filled and update according to the price changes. This in turn reduces the `Impermanent Loss` or `Divergence Loss` that the LP would have to take.

### <em>How does it work?</em>

By updating positions according to the price changes and concentrating liquidity around the current price the possible gains are maximized while greatly reducing the capital exposure to an eventual asset devaluation risk. The tighter the range that is set for a `Concentrated Liquidity Position`, the greater the fee revenue will be for that LP, and vice-versa. 

The liquidity used to execute swaps will be used from different LPs according to price fluctuations. Being that said, it can be established that users that execute swaps are making trades against the aggregated liquidity from all liquidity positions covering the current price, so it doesn't make a difference to takers which liquidity is being taken in said swaps.

<br/>
<br/>
<br/>