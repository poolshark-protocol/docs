# Price Pools
<!-- Price Position with split buy/sell side hovering around 1600 DAI/ETH -->
Price Pools operate in a similar manner to a Bidirectional Automated Market Maker.</br>

* If the market wants ETH, the pool takes DAI and increases the ETH to DAI price.
* If the market wants DAI, the pool takes ETH and decreases the ETH to DAI price.

The main difference is that there is a split buy-side and sell-side to represent each trading direction.

This enables Price Pools to enforce `price priority`, where the best priced liquidity is accessed first.

</br>
![Range Order 1](range-order2.png){: .center style="width:60%"}
</br></br>

Price Pools therefore allow users to undercut the current market price and receive priority for doing so.

In offloading a large position before a large market move, it would be ideal to slightly undercut the market price.

### **Price Pool Use Cases**

</br>
> **<em>Use Case #1: Quick Entry</em>**
> </br></br>
> <em>Alice wants to sell ETH from 2000 to 1980 DAI per ETH.</em>
> </br>
> <em>The current price of ETH is 2000 DAI per ETH.</em>

</br>
For this `Price` position:

* `lower` bound would be 1980
* `upper` bound would be 2000

The user would start offering up DAI to the market when the price of ETH is at 1980.

If this is the best price on the market, traders will naturally gravitate towards the Price Pool in order to source their liquidity.

This is great for large traders who are unwilling to accept slippage on the market, as they can wait until their liquidity is prioritized in order to capture the exact execution price they desire.


Mechanism to understand:
```
- Choosing a Range Bound
- Claiming Position Rewards
```
## Choosing a Range Bound

### Taking Profit
<!-- add subtext below image -->
If you are seeking to take profit over some price range, Price Pools are ideal given all the liquidity traded into your position will be retained. The `lower` and `upper` bound will mark the starting and ending price across which your position will trade from the input token to the output token.

### Seeking Entry
For users looking to fish entry points within some range, Price Pools can be utilized to set a range in which to enter your position. Due to the buy-and-hold nature of directional liquidity, users can retain any filled liquidity within their set range bounds.


## Claiming Position Rewards

The way in which `directional liquidity` tracks how much of the user's position has been filled is by using the value `feeGrowthGlobalIn`. That is to say that we know the highest tick at which the user got filled at based on this value. If the `accumEpochLast` of a given tick is higher than when the user minted their `Position`, we know that tick has been reached since the user's position got opened. This is the crux of how Directional AMMs (DAMMs) work.

<br/><br/>