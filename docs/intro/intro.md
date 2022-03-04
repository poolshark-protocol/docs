# Introduction

Core Concepts

At the most basic level, the main focus of the DCEX protocol is to group common execution into bulk tasks, while being cost and time efficient. While this is not a new solution to an old problem, it does utilize a different core design than that in current production or being talked about in main-stream crypto news. Let’s talk about a few solutions that we have seen or that have been proposed as an alternative then finally the new solution (DCEX)

Solution A: is utilizing a sub-chain such as arweave as a storage layer since gas costs are much cheaper in sub-chains compared to ETH mainnet, these solutions work by using decentralized services and chains to store the data, but the scalability can be questioned since they are still relying on cost of gas of the sub-chain to not succeed the price people are willing to pay. The sub-chains try to offset this problem by modeling new and interesting gas models (Needs more research).

Solution B: It may sacrifice decentralization to negate the gas of a sub-chain by utilizing events mixed with off-chain bots to relay back on-chain when conditions are met. The most obvious example of this is a centralized exchange like Binance or Coinbase, you interact with their service through an API, all balances are stored in shared wallets where the keys are unknown to the end user, and each individual user’s balance is known through tracking token deposits and spends which are then stored in some database. But all execution that needs to happen, will be executed on the relevant chain.

Solution DCEX: By combining the previous solutions ideas into a new model, we are able to have the ambiguity of full decentralization, execution being requested then executed on the relevant chain, and minimal costs (compared to current on-chain solutions). Since the solution is a combination of the above, it also shares some of the pros and cons of the above, to use the protocol you have to deposit into the contract, similar to Solution B. It utilizes a decentralized indexing service, The Graph, whereas Solution A utilizes sub-chains, but these are used in quite similar ways.

The base actions required to interact with a DCEX protocol are as follows:

1. Optional: Deposit ERC-20 token into the DCEX-ERC20-Core contract via deposit(IERC20 depositToken, uint256 depositAmount)
    1. When depositing ETH, utilize msg.value along with any other token you wish to deposit.
2. Make an action request, either through a Module or through the Core
For example, you want to Transfer DAI to your friend, you can call the core’s  transfer(address transferToken, uint256 transferAmount, address receiver) function, if the receiver doesn't have an account it will create one for them, thus allowing the receiver to ‘redeem’ their token simply by using the DCEX protocol, or withdrawing to an external address


--8<-- "docs/commons/abbreviations.md"