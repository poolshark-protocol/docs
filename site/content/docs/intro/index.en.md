---
title: Introduction
some_url: https://github.com/daifoundation/maker-otc
---
# Introduction

># **What is OceanBook?**

The OceanBook protocol is a peer-to-peer decentralized exchange which introduces efficient <em>price-time priority</em> into the world of decentralized exchanges.

It has elements of a traditional `Central Limit Order Book (CLOB)` as well as that of an `Concentrated Liquidity Market Maker (CFMM)` (e.g. Uniswap v3). Users will be able to have all the typical features they would usually expect along with ways to limit exposure to a single side.

[image of oceanbook]

<em>Features unique to OceanBook:</em>
```
> Directional LPing for single-sided risk
> Priority Queue to capture fees on large trades
> Automated closing of liquidity positions (optional)
```

<br/><br/>


<br/><br/>


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







