# Execution

## What It Does

Execution on-chain is required to reflect any requests users make both on-chain and off-chain. In the case of the GroupSwap feature, multiple users come together to fill a gas tank for a single swap on-chain. 

The actions taken on-chain utilize data originationg from The Graph Network. This data connection is made possible by Polywrap resolvers that run on Gelato Network nodes and query data from The Graph.

Polywrap resolvers have a basic yes/no 'checker function that is run to determine if anything needs to be done on-chain. For example, if a gas tank is full for a swap pair, the checker function will return true and pass the payload of data needed to execute the swap on-chain.

The PoolSharks Team has built a DEX aggregator that will handle the liquidity sourcing in the case of the GroupSwap feature. As more features are integrated with the PoolSharks Protocol, more contracts will be required for the purposes of routing common requests on-chain and finding the most cost-effective path.

## Abstraction

The Execution Layer abstracts away users having to set their own gas price. The team hopes in the future to have reliable trustless data that will enable setting Smart Slippage on behalf of users based on currently volume and liquidity availability. At this layer the goals are focused around providing a 'mainstream transaction' that everyday users can pariticpate in.

## User Functionality

## Production Requirements


--8<-- "docs/commons/abbreviations.md"