# Oracles

### Why use oracles?

Oracles are crucial for the proper functioning of the protocol since accurate and up-to-date price quotes are needed to assure the final exchange in a swap is respected according to the swap quote the end user is getting for taking liquidity.

### What is TWAP?

`TWAP` stands for `Time Weighted Average Price` which is the measure of an assets' average price over a given time interval. The goal of using `TWAP` is optimizing a trade's average price over the course of the selected time interval.

### How does it work?

The oracle will track the cumulative logarithmic sum between the current price tick and the first tick in the selected time interval in a `Geometric Mean TWAP`. In other words, the current price is derived from an arithmetic sum mean. To determine this mean, two observations are retrieved and the difference is obtained by subtracting the first observation from the current one and dividing said result by the elapsed time. 

<br/>
<br/>
<br/>