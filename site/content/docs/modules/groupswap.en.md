# GroupSwap Module

GroupSwap provides the functionality of allowing users to split gas costs of an on-chain DEX swap. Once the gas tank for a pair fills up, meaning the anticipated gas cost is covered, a swap will execute on-chain. This swap execution will emit an event and redistribute the output token evenly directly based on the input token amount.

[Diagram here to detail GroupSwap process]

The benefits of this approach are the following:

1) Eliminate users managing complex swap parameters (e.g. slippage).
2) Scale infinitely a single on-chain transaction based on the number of user requests.
3) Reduce gas usage of users at scale by up to 80%
4) Provide a more reliable swap transaction by setting gas price on behalf of users

Normally users whom have to compete for block space on a complex transaction like a swap. Instead, PoolSharks enables users to coordinate and as a result have a more reliable execution.

