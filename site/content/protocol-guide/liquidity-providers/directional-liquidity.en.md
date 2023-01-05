# Directional Liquidity

### <em>How do I create a Directional Liquidity ?</em>

`Directional Liquidity` refers to the direction the LP is going to take when entering a pool (eg. from `ETH` to `DAI`). It's similar to `Concentrated Liquidity` in the way that makers provide liquidity for a given price range, but differs by taking `Single-Sided Liquidity`, i.e. the liquidity curve only moves one way for the asset provided.

### <em>What is the main goal of using it?</em>

By providing liquidity in a certain direction, users are able to benefit from the `Impermanent Loss` reduction that `Single-Sided Liquidity` brings by not needing to deposit an equal ratio of assets both ways and thus being subject to losses due to said ratio changing over time.

### <em>How does it work?</em>

Let's say a `Liquidity Provider` wants to deposit 1 ETH to DAI in a pool from 1400 to 1200 DAI with a fee tier of 5 `Basis Points`. If a trader wants to swap `ETH` into `DAI` in this price range, the LP will get priority over other LPs with bigger ranges for this price direction. If the LPs' liquidity is used in the swap the 5 BP over the amount of tokens swapped will be accrued as fees (e.g. if a user swaps 10 ETH into DAI and there is enough liquidity to fill the order the LP will take at least 60 `DAI` and at most `70` DAI assuming the minimum and maximum prices of the range are maintained).