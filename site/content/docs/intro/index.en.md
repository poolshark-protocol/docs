---
title: Introduction
some_url: https://github.com/daifoundation/maker-otc
---
# Introduction

># **What is OceanBook?**

The OceanBook protocol is a peer-to-peer decentralized exchange which introduces efficient <em>price-time priority</em> into the world of decentralized exchanges.

It has elements of a traditional `Central Limit Order Book (CLOB)` as well as that of an `Concentrated Liquidity Market Maker (CFMM)` (e.g. Uniswap v3). Users will be able to have all the typical features they would usually expect along with ways to limit exposure to a single side.

<em>Features unique to OceanBook:</em>
```
> Directional LPing for single-sided risk
> Priority Queue to capture fees on large trades
> Automated closing of liquidity positions
```

The core objective is to provide innovative mechanisms for on-chain market making.
<br/><br/>


># **Slippage On Constant Function Market Makers**

For traders exchange tokens on CFMMs (e.g. Uniswap v3), they are often subject to increasing slippage on larger trades.

This `slippage` is derived on the variance in the token reserves and is ultimately a passive pricing model to predict what price the liquidity provider should exchange at.

![Screenshot](slippage.jpeg){: .center style=""}

When this slippage exceeds the price on another liquidity source (e.g. a centralized exchange), arbitrageurs
will bring the price on the AMM pool up to par.

What this demonstrates is that passive pricing from Automated Market Makers cannot surpass the efficiency of active pricing from a Central Limit Order Book. The scalability issues of the blockchain are what prevent this limitation from being surpassed.

The OceanBook Protocol enables market makers to undercut the current market price and receive fees accordingly. 

Any liquidity that is added to the Priority Queue (skip to section) will result in 0% slippage for traders. The positive tradeoff for the Market Maker is they receive 100% of fees for liquidity provided.
<br/><br/>
># **The Liquidity Fragmentation Problem**

The Liquidity Fragmentation Problem for on-chain orderbooks can be described as the following:

> **<em>Y liquidity cannot be guaranteed for X gas spent.</em>**

This is due to the fragmentation of liquidity between orders.

Takers encounter this problem namely when there are zero restrictions on maker order size.

It doesn't make sense to have a small maker order in a traditional CLOB on-chain because the amount of fees you will make in return will not surpass the amount of gas you spent to make a single order.

### **Mistakes of the Past: Where Decentralized Orderbooks Have Fallen Short**

There is one guiding principle which sets OceanBook apart from other on-chain orderbook protocols.

This is the ability to have a `closed-form expression`, meaning there is a finite amount of computation that will take place at each price point.

> **<em>For X amount of gas spent, a taker must receive Y liquidity.</em>**
<br/>
<br/>

OceanBook is designed specifically to solve this core UX problem.
#### **Maker OTC by the Dai Foundation**

[Maker OTC](https://github.com/daifoundation/maker-otc) was an attempt at an on-chain orderbook with the following in its `README.md`:

```
Design Consideration

The protocol uses an on-chain order book and matching engine. The primary advantage
of such approach is that the liquidity is available for other smart contracts 
that can access it in one atomic ethereum transaction. The second advantage is
that the protocol is fully decentralized without any need for an operator.

Order book for each market is implemented as two double-linked sorted lists, one
for each side of the market. At any one time the list should be sorted.

The second important design choice is the use of the Escrow model for Makers - 
every order on the order book needs to be "backed up" by the liquidity that is
escrowed in the contract. Although such approach locks down liquidity, it 
guarantees zero-risk, instantenous settlement.
```
<br/>
The main downfalls of Maker OTC:

- Offer iteration is expensive
- Doubly linked list maintenance
- No correlated market with continuous liquidity
<br/>
<br/>

#### **The Liquidity Fragmentation Problem**
<br/>
Assume that accessing each order's liquidity involves 4 storage reads and 2 storage writes.

4 * SLOAD cost + 2 * SSTORE cost = 18,400 gas units

Accessing each order's liquidity will cost 18,400 gas units on storage alone.

A Uniswap v3 swap will comparitively be ~127,000 gas units at a single price tick.

<br/>

![Screenshot](maker-otc-gas.png){: .center style=""}
<br/>
<br/>

Once we have accessed more than 3 orders we have already exceeded this gas cost.

Consider the base transaction fee is 21,000 gas units and 2 ERC-20 transfers is 60,000 gas units.

21,000 + 60,000 + 18,400 * 3 = 136,200 gas units (107% of Uniswap v3 swap)
<br/>
<br/>
#### **Non-Deterministic Behavior**
Each offer has a fragmentation of the liquidity at a given price.

Instead of aggregating all the orders at a given price, we have to do `N` loads.

This `N` value could be unbounded and thus we encounter non-deterministic behavior.

*Note: markets could be disrupted by extreme liquidity fragmentation (i.e. many small orders).*

If we have no minimum order size, this can easily explode taker gas costs.

All it would take is the placement of thousands of small offers.

###<em>Maker OTC Conclusion:
The taker is not guaranteed to spend X gas for Y liquidity.</em>
<br/>
<br/>

![Screenshot](maker-otc-gas.png){: .center style=""}
<br/>
<br/>

### **How does the OceanBook protocol compare to a traditional centralized exchange orderbook?**

In comparison to a centralized exchange orderbook, on-chain limit order books cannot be equally expressive without encountering scalability issues.

This means that each `Book` contract will support limited precision with respect to the possible exchange rates between tokens.

The goal is to strictly limit the amount of on-chain storage access in order to maximize volume for the benefit of everyone.

In order to achieve this we must maximize deterministic behavior.

Traditionally this is why AMMs have worked quite well, and the same rules apply here.

This means accomodating for trades of different sizes separately as the amount of data each of these will load can be drastically different.

More details on how we solved for this will be released alongside the launch of public testnet.

<br/>
<br/>







