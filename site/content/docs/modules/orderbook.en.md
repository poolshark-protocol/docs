# Orderbook Module

The Orderbook Module functions as a list of buy and sell orders earmarked at a specific price. Compared to an AMM, this model leads to a better price discovery due to the non-passive nature of market activity.

Within the PoolSharks Protocol, orders are submitted on-chain. Once picked up by an Indexer on The Graph Network, the Subgraph attempts to match the user's order with another existing order. In the case there is no match, the order is left in the orderbook to be filled by another incoming order.

You can follow the process for handling incoming orders below:

[DIAGRAM HERE TO ILLUSTRATE ORDERBOOK PROCESS]