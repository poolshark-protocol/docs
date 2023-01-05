# Range Pools
<!-- Price Position with split buy/sell side -->
Range Pools are similar to what users can expect from bidirectional liquidity: LPs can range bound their liquidity. This results in more liquidity being available close to market price, increasing trading fees accrued from such a position.

Range Pools here have one unique feature improving composability with other DeFi protocols: `Default Ranges`. 

![Fungible Range Pool Positions](range-pool-erc20.png){: .center style="width:85%"}

To put it simply, Range Pools contain many small constant function curves between each price point, commmonly referred to as a `Tick`. 

The main difference with Range AMMs is that there are many price ranges within one `PoolsharkRangePair` contract. Each of the smaller price ranges will have reserves based on liquidity active within that `Tick`. Within each `Tick`, the pool functions exactly the same as what users have come to know from Constant Function Market Makers.

Now, let’s try to visualize it. What we’re saying is that we don’t want the curve to be infinite. We cut it at the points aa and bb and say that these are the boundaries of the curve. Moreover, we shift the curve so the boundaries lay on the axes. This is what we get:

Mechanism to understand:
```
- Choosing a Range Bound
- Claiming Position Liquidity
- Claiming Fees Accrued
```
## Choosing a Range Bound

### Taking Profit
<!-- add subtext below image -->
If you are seeking to take profit over some price range, Price Pools are ideal given all the liquidity traded into your position will be retained. The `lower` and `upper` bound will mark the starting and ending price across which your position will trade from the input token to the output token.

### Seeking Entry
For users looking to fish entry points within some range, Price Pools can be utilized to set a range in which to enter your position. Due to the buy-and-hold nature of directional liquidity, users can retain any filled liquidity within their set range bounds.


## Claiming Position Liquidity

Depending on the current price of the pool, the user will be able to withdraw their position accordingly:

* `price` < user's `lower` tick: 100% of user liquidity will be in `token0`
* `price` > user's `upper` tick: 100% of user liquidity will be in `token1`
* `price` > user's `lower` tick AND `price` < user's `upper` tick: a mix of the user's liquidity will be both in `token0` and `token1`

## Claiming Fees Accrued

The way in which `Range Pools` track how much of the user's position has been filled is by using the value `feeGrowthGlobal`. Depending on where the current tick is will determine what liquidity is withdrawn from the pool.

Fee accounting is tracked with the `feeGrowthGlobal0` and ``feeGrowthGlobal1` values present on the `upper` and `lower` tick representing the user's Position. Global fees generated represent 1 unit of liquidity, so to get the fees belonging to a single `Position`, we will multiply by that `Position`'s liquidity amount. 

Fees accumulated outside of a price range are tracked when a tick is crossed. This allows us to simply calculate fees accumulated below the lower tick and then fees calculated above the upper tick.

`feeGrowthGlobal0` and ``feeGrowthGlobal1` are on a per liquidity unit basis, so this value is simply multiplied by the amount of liquidity contained in a Position to determine the fees owed to that specific Position.


<br/><br/><br/>