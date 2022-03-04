# Data Ingestion

## What It Does

Once events occur on-chain, the Core ERC20 Subgraph receives record of what happened and reflects those changes via event handlers.

For example, in the case of a Deposit event, the following data is emitted:

`Deposit (index_topic_1 address user, index_topic_2 address token, uint256 amount)`

The Deposit handler will assign the balance `amount` to the account `user` for the contract address `token`.

The balance is now spendable by the user, meaning they can request a withdraw, groupswap, etc. Once spendable balance has been associated with a user request, the balance will be made nonspendable in the amount requested by the user. This prevents the classical double-spending problem from occurring. 

In our system design, we typically refer to this process as making a `reservation`. Balance is nonspendable until the order is cancelled by the user or the order is fulfilled.

## Abstraction

Here the Core ERC20 Subgraph is abstracting away the costs of storing all the accounting and user request information on-chain and instead opting for the data to be availalble via The Graph Network.

## Production Requirements

Indexing speed here is a potential issue, however Ethereum is limited to 15 TPS which bottlenecks the amount of events the DCEX Subgraphs will be processing.

One solution here is to have the team run its own node within The Graph Network, which will to a large guarantee real-time availability of Subgraph data.

The other potential pitfall is indexing correctness, for which a process needs to be developed around creating disputes for [Proof of Indexing (POI)](https://thegraph.com/docs/en/indexing/#what-is-a-proof-of-indexing-poi) when data is indexed in an invalid manner.

--8<-- "docs/commons/abbreviations.md"