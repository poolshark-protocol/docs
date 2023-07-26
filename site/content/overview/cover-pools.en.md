# Cover Pools
<!-- Cover Position alongside Range Position -->
Cover Pools allow you to create positions to increase exposure to a specific token conditional on it increasing in price on a given pair.</br>

A position on a cover pool can be considered a stop-loss (SL) order. In this case, you can view your range as the ranged version of the “trigger point” for the order.

Like other AMM positions, the cover pool works with discrete price ticks that in this case define the liquidity to be auctioned, the trigger point for the liquidity, and the starting price for the auction of the liquidity within that price tick.

When you provide liquidity to a cover pool position across a range it is split across the ticks within the trigger range you have selected.

So when the reference price reaches or passes a price tick with liquidity it initiates the Dutch Auction for the liquidity within that price tick.

If a position is or has been in range on a [bidirectional automated market maker](https://docs.poolshark.fi/overview/glossary/#bidirectional-automated-market-maker) it increases the exposure to the token dropping in price or has all exposure to the token dropping in price.</br>

* If the market wants ETH, the pool takes DAI and increases the ETH to DAI price
* If the market wants DAI, the pool takes ETH and decreases the ETH to DAI price.
<br/><br/>
![Range Order 1](cover-vs-range.png){: .center style="width:75%"}
<br/><br/>
This allows them to function as a hedging tool if the user wants to enter or exit an **ERC-20** token over some range. 

If this was attempted using a position with a fixed price such as a limit order (as done when providing liquidity) the position will either underprice the assets or it won't be filled.

Cover pools allow you to create a position to provide liquidity at a set price and when the TWAP price nears the liquidity becomes available to trade. The liquidity is then a part of a [Dutch Auction](https://docs.poolshark.fi/overview/glossary/#dutch-auction).

Cover Pools operate with a [Gradual Dutch Auction (GDA)](https://www.paradigm.xyz/2022/04/gda) meaning that you can start at the price indicated by the current price tick of your position and begin to offer a more discounted price until it is accepted by the market.

As a **Range Order**, Cover Positions will unlock periodically unlock liquidity across a price range as the [**Time-Weighted Average Price**](https://docs.poolshark.fi/overview/glossary/#time-weighted-average-price-twap) (TWAP) increases or decreases (indicated by the user).

This is because we don't want the pool to unlock liquidity due to high-frequency market volatility which will be closed out in an extremely short time due to arbitrage.


## Applications (non-exhaustive)

### Covering Potential Impermanent Loss
<!-- add subtext below image -->
If you are seeking to cover impermanent loss dynamically as the price moves, it is ideal for your lower and upper bound to match your current position on either Uniswap v3 or Poolshark. It is okay to put the same upper and lower bound as on your original Range Position NFT. The `PoolsharkCoverPair` contract will automatically calculate how much input token you should transfer into the pool based on the currently valid price range.

If the user wants to increase capital efficiency, they can either increase the lower bound or decrease the upper bound so that less upfront capital is required.

Rather, Cover positions are meant to decrease the exposure of one asset and increase exposure to another as the price of the initial asset becomes worse. This is a way for LPs to hedge a portion of their portfolio in the case that the market price moves against a given asset.
</br></br></br><br/><br/>
![Range Order 1](cover_position.png){: style="width:100%"}
</br></br>

Assuming the user wants to cover any potential impermanent loss, this range should match their original LP position and the value of the position should also be equal to more accurately cover impermanent loss.

### Trading Conditional on Price Changes
For users seeking to trade into an asset starting at some price (example in the image below), they can set the lower bound as the point where they want to start transitioning from the input token to the output token. 

The Cover Pool will unlock liquidity at each price point based on the total amount of liquidity available in the pool for a given pair direction.

Capital efficiency can be improved by selecting a smaller range over which to trade to the desired output token.

Cover LP Positions can also be used to deleverage long or short positions before getting liquidated.

### Dynamic Rebalancing of Positions

A position on a cover pool can also be used to dynamically rebalance your portfolio while prices change.

For example, if you are looking to rebalance your portfolio as Token A is decreasing in value to reduce exposure to token A or expressed inversely increase exposure to token B due to token B increasing in value. The key point is that it rebalances from one token into another due to the price change. 

### Deleveraging to Avoid Liquidation

Deleveraging is the process of reducing leverage or borrowing to decrease the risk of liquidation. When users borrow against their collateral on DeFi protocols, they are susceptible to liquidation if the value of their collateral falls below a certain threshold. By deleveraging, users reduce their borrowing and decrease the likelihood of their positions being liquidated.

By moving from a more risky asset into a more stable asset it increases the required price decrease to be liquidated. All this can be accomplished while the position changes its composition from a risky asset to a stable asset without needing to remove the collateral.

With lending protocols that accept cover pool positions as collateral, you can use them to lend a risky asset while being able to keep the upside potential of the collateral without needing to remove liquidity and interrupt the loan.


## How Auctions Work

To be competitive with the current market rate, the pool must have a dynamic pricing mechanism so the position is filled as soon as possible while keeping any discount at a minimum. For this, Cover Pools use Gradual Dutch Auctions to raise or lower the pool price (depending on buying or selling a token) to satisfy market demand for an asset within a trading pair in that instance.

From Paradigm's Gradual Dutch Auction article:
```
Here, the price for every auction decays exponentially according to some `decay constant`.
The starting price of each auction increases by some fixed `scale factor`.
And the starting price of the first auction is given by some `initial price`.
```

Combining these values gives us an exponentially changing market price for each tick of liquidity we auction off. The price will never deviate by more than one price tick (e.g. 0.1% for the ETH-USDC 0.05% tier).

## How Volatility Tiers Work

Volatility tiers set a few different parameters when a pool is created. These variables include the auction length, syncing fee, minimum position size, and minimum position width. 

Auction length is the number of blocks until the next auction can be triggered by a price change. 

A syncing fee is for when an auction goes unfilled and it needs to be moved to the next price tick in which liquidity is added to the auction at the new price tick. 

Minimum position size is the minimum amount of liquidity required at a price tick to commence an auction. 

Minimum position width is the minimum amount of price ticks a position can span.

<br/><br/>