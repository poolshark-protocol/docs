# Aave Module

The Aave Module takes the same 'carpooling' approach as the GroupSwap module in terms of matching up transactions that will execute with the same parameters (i.e. Deposit, Liquidate, etc.) for saving users on gas and increasing transaction reliability.

A typical Aave deposit call can easily cost upwards of 250000 gas units depending on the token, which is 2x the cost of a Uniswap V3 swap. This creates a large barrier for smaller wallets that want to earn sustainable yield from a variable lending market and restricts the movement of their capital over time.