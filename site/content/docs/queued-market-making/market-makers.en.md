# Queued Market Making
## For Market Makers
A `Queued Market Maker` is a decentralized exchange structure wherein `Fungible Queues` are used to achieve <em>price time priority</em>.

The `Fungible Queues`, or `Pages`, are ordered from lowest to highest price so `Takers` seeking to access liquidity from the exchange can be filled up to their limit price.

Each `Page` has a collection of `Orders` linked to it.

<br/>
![Screenshot](maker-qmm.png){: .center style=""}
<br/>
<br/>
In the above figure, each person will represent a `Maker` order in a queue.

Alice has the first `Order` in the (4000 DAI : 1 ETH) `Page` will starts at `0` and ends at `100`.

Bob has the first `Order` in the 4000 DAI : 1 ETH `Page` will starts at `0` and ends at `100`.

Since a page exists for 3000 DAI (i.e. a lower offer), the volume counter for the 4000 DAI page will remain `0` until all the orders from the 3000 DAI page are filled.

The benefit in this exchange model from the perspective of `Market Makers` can be summarized in a few key points:

```
1. Fees are NOT shared with liquidity providers that provide more liquidity 
   than is needed to fill Taker orders.
2. Since Makers are filled FIFO, they can claim their completed order
   immediately along with any fees generated from the order flow. This
   allows for subsidization of the next set of orders placed on the exchange.
3. In order for another Market Maker to front-run an existing Order, they must
   offer a lower price and take a loss on any liquidity provided.
```

<br/>
<br/>
<br/>