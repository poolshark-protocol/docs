# Data Ingestion

## What It Does

Once events occur on-chain, the Core ERC20 Subgraph receives record of what happened and reflects those changes via event handlers.

For example, in the case of a Deposit event, the following data is emitted:

`Deposit (index_topic_1 address user, index_topic_2 address token, uint256 amount)`

The Deposit handler will assign the balance `amount` to the account `user` for the contract address `token`.

The balance is now spendable by the user, meaning they can request a withdraw, groupswap, etc. Once spendable balance has been associated with a user request, the balance will be made nonspendable in the amount requested by the user. This prevents the classical double-spending problem from occurring. 

In our system design, we typically refer to this process as making a `reservation`. Balance is nonspendable until the order is cancelled by the user or the order is fulfilled.

## Abstraction

## Production Requirements
