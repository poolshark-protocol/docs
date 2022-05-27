# Introduction

## What is OceanBook?

PoolSharks OceanBook aims to deliver a fully on-chain FIFO matching engine for limit orders, which is gas finite and optimized to be fully viable on L1 Ethereum Mainnet.

To fully understand what OceanBook proposes, we have to understand the markets, how an Orderbook works, and what the tradeoffs are versus an Automated Market Maker (AMM). 

After we're aware of the differences for both traders and LPs, we can start to comprehend where this new market maker model really shines.

### Current Decentralized Exchanges 



### Solution B
It may sacrifice decentralization to negate the gas of a sub-chain by utilizing events mixed with off-chain bots to relay back on-chain when conditions are met. The most obvious example of this is a centralized exchange like Binance or Coinbase, you interact with their service through an API, all balances are stored in shared wallets where the keys are unknown to the end user, and each individual user’s balance is known through tracking token deposits and spends which are then stored in some database. But all execution that needs to happen, will be executed on the relevant chain.

### Solution DCEX
By combining the previous solutions ideas into a new model, we are able to have the ambiguity of full decentralization, execution being requested then executed on the relevant chain, and minimal costs (compared to current on-chain solutions). Since the solution is a combination of the above, it also shares some of the pros and cons of the above, to use the protocol you have to deposit into the contract, similar to **Solution B**. It utilizes a decentralized indexing service, The Graph, whereas **Solution A** utilizes sub-chains, but these are used in quite similar ways.

The base actions required to interact with a DCEX protocol are as follows:

1. Optional: Deposit ERC-20 token into the DCEX-ERC20-Core contract via `deposit(address depositToken, uint256 depositAmount)`
    1. When depositing ETH, utilize `msg.value` along with any other token you wish to deposit.
2. Make an action request, either through a Module or through the Core
For example, you want to Transfer DAI to your friend, you can call the core’s  `transfer(address transferToken, uint256 transferAmount, address receiver)` function, if the receiver doesn't have an account it will create one for them, thus allowing the receiver to ‘*redeem*’ their token simply by using the DCEX protocol, or withdrawing to an external address

[Diagram of DCEX hierarchy]

--8<-- "docs/commons/abbreviations.md"