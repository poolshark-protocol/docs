# Introduction

## What Is a Fungible Queue?

Fungible Queues provide a means of telling Market Makers, also referred to as Liquidity Setters, when their order is filled.

They are developed with the quality of fungilibity in mind, meaning that all the assets being placed onto the same queue are treated in an equal manner.

This data structure helps us achieve the quality of "price time priority" wherein each Market Maker has a queue position.

See [References](http://market-microstructure.institutlouisbachelier.org/uploads/91_7%20MOALLEMI%202014-12-paris-mm-queue-value.pdf) on why queue position in a limit order book matters.

<em>In the end we only need a few pieces of information to have an operational Maker/Taker side:</em>

- the exchange rate for the specific queue
- the total volume of maker orders created
- the total volume of taker orders executed

When things are of a homogenous nature in a smart contract, there is no need for us to read multiple pieces of data.

<em>Thus...</em>

If we are aware of how much liquidity is available at a certain price on a token pair, **there is no need to read each individual maker order.**

This is what makes the concept of Fungible Queues unique.

<br/>
<br/>
<br/>


