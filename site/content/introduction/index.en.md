---
title: Introduction
some_url: https://github.com/daifoundation/maker-otc
---
># **What is Poolshark?**

The `Poolshark Protocol` is a set of smart contracts which implements `directional liquidity`, an alternative to the often popular `bidirectional liquidity`, seen in popular AMMs such as Uniswap and Curve.

The concept of `directional liquidity` along with `bidirectional liquidity` are intended to offset each others' weaknesses. Buy-and-hold strategies are enabled by `directional liquidity` while `bidirectional liquidity` focuses on fee capture from the point of the liquidity provider.

<!-- MEDIUM: Image of Poolshark logo with Cover Pool, Price Pool, and Range Pool represented -->

Bidirectional liquidity, what users have come to know of AMMs, allows trades in both directions. This is great for capturing fees due to the continuous liquidity. 

In the case there is significiant price divergence (i.e. impermanent loss), the collateral value of such an LP position may be less than that of a pure buy-and-hold strategy. This is where `directional liquidity` can positively impact an LP's profitability by reclaiming lost profits.  
</br></br>
<em>Bottom line: Directional liquidity enables buy-and-hold strategies for liquidity providers to offset directional risks in their portfolio such as impermanent loss.</em>
</br></br></br>
<em>Expected additional losses from Impermanent Loss:</em>
![Screenshot](divergent-loss.png){: .center style=""}
<!-- LOW: replace this image with our own -->
As a one-way liquidity strategy, directional liquidity is intended to offset losses elsewhere in an LP's portfolio, which could include the following:
</br></br>
```
* The potential for impermanent loss as token prices diverge

* Protection against liquidation

* Enter and exit the market quicker with less slippage
```
</br>

Due to this capability, directional liquidity enables LPs to more safely rebalance their position whilst covering the impermanent loss they experience when rebalancing.

At a high-level, directional liquidity has the `x*y=k` design elements of a `Range AMM` (e.g. Uniswap v3), where LPs are free to choose a range in which to allocate their capital for maximum efficiency.

Directional Liquidity allows users to:

* Choose the trading direction
* Protect against adverse price movements
* Offer better prices than other pools

## **Choose the Trade Direction**

In a traditional liquidity pool, LP positions trade both directions.

Traders making swaps can trade from ETH to DAI or vice versa with users' LP positions.

Here with directional liquidity, providers will specify the direction, meaning the user will either accept incoming ETH or DAI but not both.

The outcome is that liquidity that the LP can better capture price movements without having to rush to close their LP position in the desired state (i.e. the current generation of `Range Orders`).

## **Protect Against Adverse Price Movements**

Due to the buy-and-hold nature of directional liquidity, LPs are not impacted by price movements in the opposing direction.

If an LP is trading from ETH -> DAI with a range of 2000 to 2200, a price movement to 2100 with a return to 2000 will still result in the LP being filled to the price of 2100.

Traditional AMMs which support bidirectional LPing would result in the position trading from ETH into DAI and back into ETH when the price returns to 2000.

Thus, traditional AMMs require an off-chain actor to close the LP position before it stops becoming tradable. This can result in front-running and is not always desirable for a fast-moving market.

## **Offer Better Prices Than Other Pools**

Due to the design of traditional AMMs, there is no split `buy-side` and `sell-side`.

To put it into simpler terms, we use one liquidity curve to represent ETH->DAI and DAI->ETH.

With `directional liquidity`, we use separate liquidity curves to represent each trading direction.

What this enables is for LPs to undercut the market price on either side.

An LP could provide the highest price to buy ETH at and enter the market before a large move up in the ETH price. Likewise, an LP could provide the lower price to sell ETH at and exit the market before a large downturn.

## **The Two Flavors of Directional Liquidity**

Directional Liquidity comes in two flavors:

- Cover pools
- Price pools

[`Cover Pools`](cover-pools) are meant to "cover" or "hedge" a position in the user's portfolio.

[`Price Pools`](price-pools) give pro-rata price priority for each trading direction.

Use cases for each can be observed on their respective pages.




### **Wrapping Up The Introduction**
<br/>
Simply said, we are excited to see how liquidity providers leverage directional liquidity to capture more profits on their LP positions and improve their liquidity operations.

<br/>
![Screenshot](book_screenshot.png){: .center style=""}
<br/>

With these added features, liquidity providers can customize their risk profile to match the current price action in the market.

<em>Directional LPing</em> allows for one-way fills similar to a traditional limit order, whereas current LP positions will trade both ways.

DeFi protocols are often the largest liquidity providers in the ecosystem, so we're excited to see how our community and ecosystem can build solutions around protocols that are seeking to greater improve their profitability and runway for the coming years.

If you would like to contribute or have any questions, don't hesistate to [open an issue on Github](https://github.com/poolsharks-protocol/docs/issues)!

<br/><br/><br/>








