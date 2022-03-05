# Execution

## What It Does

Execution on-chain is required to reflect any requests users make on-chain. In the case of the GroupSwap feature, multiple users come together to fill a gas tank for a single swap on-chain. 

The actions taken on-chain utilize data from The Graph Network. This data connection is made possible by Polywrap resolvers that run on Gelato Network nodes and query data from The Graph.

Polywrap resolvers have a basic true/false 'checker' function that is run to determine if anything needs to be done on-chain. For example, if a gas tank is full for a given swap pair, a swap will be executed on-chain and the output token will be distributed evenly amongst the participants based
on the amount of input token they contributed to the pool.

The PoolSharks Team has built a DEX aggregator that will handle the liquidity sourcing in the case of the GroupSwap feature. As more features are integrated with the PoolSharks Protocol, more contracts will be required for the purposes of routing common requests on-chain and finding the most cost-effective path.

## Abstraction

The Execution Layer abstracts away users having to set their own gas price. Currently this gas price is set by Gelato. The PoolSharks Team is exploring
leveraging of data to set other parameters such as slippage on behalf of users.

## User Functionality

The Gelato Network will enable asset transfer to be automated either on behalf of a user or a set of user requests. Withdraws will be processed in this manner where a withdraw request is submitted and then finalized on-chain once processed by a Gelato Polywrap bot. Trustless data is a key factor here to ensure the data being served matches what users submitted on-chain.

Routing requests to other on-chain protocols is also handled by Gelato Polywrap bots, such as in the case of a Uniswap swap or an Aave deposit call. Events are then emitted from the resulting on-chain action and then reflected back in the Core ERC20 Subgraph for syncing purposes.


## Production Requirements

Currently, anyone can create a task for a smart contract function that is executable by the Gelato Network. However, in our case we need to limit execution of our Core ERC20 contract functions to whitelisted modules only. Certainly we don't 'Bob down the street' executing our smart contract functions and passing bad data.

Additionally, the protocol will ideally deploy immutable Gelato tasks in an effort to make the system behave more like a smart contract. Censorship resistance, immutability, and non-custodial are all descriptors we intend to reflect in the design of this protocol.

--8<-- "docs/commons/abbreviations.md"