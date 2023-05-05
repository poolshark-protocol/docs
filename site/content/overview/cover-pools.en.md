# Cover Pools
<!-- Cover Position alongside Range Position -->
Cover Pools allow you to create positions to increase exposure to a specific token conditional on it increasing in price on a given pair.</br>

* If the ETH price increases, the pool sells DAI and increases the amount of ETH exposure
* If the ETH price decreases, the pool sells ETH and increases the amount of DAI exposure

If a position is or has been in range on a [bidirectional automated market maker](##-bidirectional-automated-market-maker) it increases the exposure to the token dropping in price or has all exposure in the token dropping in price.</br>

* If the market wants ETH, the pool takes DAI and increases the ETH to DAI price
* If the market wants DAI, the pool takes ETH and decreases the ETH to DAI price.

![Range Order 1](cover-vs-range.png){: style="width:90%"}

This allows them to function as a hedging tool if the user wants to enter or exit an **ERC-20** token over some range. 

If this was attempted using a position with a fixed price such as a limit order (as done when providing liquidity) the position will either underprice the assets or it won't be filled.

Cover pools allow you to create a position provide liquidity at a preset price and when the TWAP price nears begin to provide the liquidity to a pool and decrease the price at a fixed rate until all liquidity is used.

Cover Pools operate with a [Gradual Dutch Auction (GDA)](https://www.paradigm.xyz/2022/04/gda) meaning that you can start at the price indicated by the current price tick of your position and begin to offer a more discounted price until it is accepted by the market.

As a **Range Order**, Cover Positions will unlock periodically unlock liquidity across a price range as the **Time-Weighted Average Price** (TWAP) increases or decreases (indicated by the user).

This is because we don't want the pool to unlock liquidity due to high frequency market volatility which will be closed out on an extremely short time period due to arbitrage.

### Cover Pool Use Cases

</br>
> **<em>Use Case #1: Averaging into a Position</em>**
> </br></br>
> <em>Alice wants to buy ETH from 2000 to 2200 DAI per ETH.</em>
> </br>
> <em>The current price of ETH is 1500 DAI per ETH.</em>

</br>
For this `Cover` position:

* `lower` bound would be 2000
* `upper` bound would be 2200

The user would start offering up DAI to the market when the price of ETH is at 2000.

The position would stop purchasing ETH after the prices crosses 2200 DAI per ETH.
</br></br>
> **<em>Use Case #2: Hedging Impermanent Loss</em>**
> </br></br>
> <em>Alice has an ETH/DAI LP Position on Uniswap v3.</em>
> </br>
> <em>Her range has `lower` bound 1000 and `upper` bound 5000.</em>
> </br>
> <em>The current price of ETH is 3000 DAI per ETH.</em>
> </br>
> <em>Alice wants to cover potential IL from 3000 to 5000 DAI per ETH.</em>

</br>
Assuming the user wants to cover any potential impermanent loss, this range should match their original LP position and the value of the position should also be equal to more accurately cover impermanent loss.

Capital efficiency can be improved by selecting a smaller range over which to trade to the desired output token.

Cover LP Positions can also be used to deleverage long or short positions prior to getting liquidated.

Mechanism to understand:
```
- Choosing a Range Bound
- Auctioning Unlocked Liquidity
- Claiming Position Rewards
```
## Choosing a Range Bound

### Covering Potential Impermanent Loss
<!-- add subtext below image -->
If you are seeking to cover impermanent loss dynamically as the price moves, it is ideal for your `lower` and `upper` bound to match your current position on either Uniswap v3 or Poolshark. It is okay to put the same `upper` and `lower` bound as on your original Range Position NFT. The `PoolsharkCoverPair` contract will automatically calculate how much input token you should transfer into the pool based on the currently valid price range.

If the user wants to increase capital efficiency, they can either increase the `lower` bound or decrease the `upper` bound so that less upfront capital is required.

Rather, Cover positions are meant to decrease exposure of one asset and increase exposure to another as the price of the initial asset becomes worse. This is a way for LPs to hedge a portion of their portfolio in the case the market price moves against a given asset.
</br></br></br>
![Range Order 1](cover_position.png){: style="width:100%"}
</br></br>

### Trading into a token
For users seeking to trade into an asset starting at some price (example in the image below), they can simply set the `lower` bound as the point where they want to start transitioning from the `input` token to the `output` token. 

The Cover Pool will unlock liquidity at each price point based on the total amount of liquidity available in the pool for a given pair direction.

## How auctions work

In order to be competitive with the current market rate, the pool must have a dynamic pricing mechanism so the position is filled before the price moves too far out of range. For this, Cover Pools use the mechanism to naturally raise or lower the current pool price every block based on supply demand dynamics.

From Paradigm's Gradual Dutch Auction article:
```
Here, the price for every auction decays exponentially according to some `decay constant`. The starting price of each auction increases by some fixed `scale factor`. And the starting price of the first auction is given by some `initial price`.
```

Combining these values gives us a exponentially increasing market price for each tick of liquidity we auction off. The price however should never deviate by more than one tick (e.g. 0.1% for the ETH-USDC 0.05% tier).

## How Volatility Tiers work

Volatility tiers set a few different parameters when a pool is created being the auctionLength, syncing fee, filling fee, minimum position width, 

auctionLength
blockTime
syncFee
fillFee
minPositionWidth
minAmountLowerPriced



<br/><br/>