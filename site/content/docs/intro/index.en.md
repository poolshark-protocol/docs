---
title: Introduction
some_url: https://github.com/daifoundation/maker-otc
---
># **What is Poolshark?**

The `Poolshark Protocol` is a set of smart contracts which introduces `directional liquidity` into the design space of AMMs, an alternative to the often popular `bidirectional liquidity`, seen in popular AMMs such as Uniswap and Curve.

Directional liquidity has elements of a `Range AMM` (e.g. Uniswap v3), where LPs are free to choose a range in which to allocate their capital for maximum efficiency.

The major difference here is that liquidity is not recycled back into the pool once traded. This enables buy-and-hold strategies from the point of the liquidity provider. Given this protocol design, user LP positions are incrementally closed as their position is filled.

Directional Liquidity comes in two flavors:

- Cover pools
- Price pools

The `Cover` position is meant to "cover" or "hedge" a position in the user's portfolio.


> <em>Example #1:</em>
> </br>
> <em>User wants to buy ETH from 2000 to 2200 DAI per ETH.</em>
> </br>
> <em>The current price of ETH is 1500 DAI per ETH.</em>

For this `Cover` position:

* `lower` bound would be 2000
* `upper` bound would be 2200

Example #2: User has an ETH/DAI LP Position on Uniswap v3 and wants to cover their IL if ETH goes up in price.
            Assume the user has a `lower` bound of 1000 and an `upper` bounce of 10000.

Since the user wants to cover any potential impermanent loss, this range should match their original LP position.

Capital efficiency can be improved by selecting a smaller range over which to trade to the desired output token.



Liquidity Positions are then aggregated together into a single pool for users to trade against.

Currently direct AMM users are forced to market buy tokens with high slippage or place a Range Order which requires an off-chain actor to close the position.

Poolshark introduces:

* Choose the trading direction
2. Protect against adverse price movements
3. Offer better prices than other pools

Let's break down each of these to understand the value this provides for LPs.

## **Choose the Trade Direction**

In a traditional liquidity pool, LP postiions trade both directions.

<br/><br/>
![Screenshot](book_screenshot.png){: .center style=""}
<br/>

With these added features, liquidity providers can customize their risk profile to match the current price action in the market.

<em>Directional LPing</em> allows for one-way fills similar to a traditional limit order, whereas current LP positions will trade both ways.

<br/><br/>








