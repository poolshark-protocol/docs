# PoolSharks Orderbook

The PoolSharks Orderbook is an on-chain central limit order book (CLOB) on Ethereum which provides an order-matching system built for everyone.Through it's permissionless nature, users can launch a pair with no upfront capital, since there is no AMM Liquidity Pool required. 

More importantly the gas costs associated with creating a new pair are reduced by more than 90% due to the minimalistic and optimal on-chain storage approach.

# Features

* Zero off-chain execution for basic limit orders
* Composable multi-hop trades between multiple pairs
* Advanced order types and features (stop loss, trailing take profit, flash crash protection, etc. via Gelato)
* Seamless IDO / token launches without upfront capital at a specified price

# Design

[Diagram]

Here are some base definitions to better help convey the design.
Book: A collection of Pages regarding to a monodirectional token pair A->B
Page: A collection of orders at a given price point
Orders: Description of a given user's trade

Pages are doubly linked list, such that you can read through the book in a given order
Orders are doubly linked lists, such that you can define who receives a trade based on volume.

When an order is fulfilled, the taker spends X amount of Token A and receives Y amount of Token B, while the maker can redeem the token at a later point in time, or use it to create a new order without redeeming!
