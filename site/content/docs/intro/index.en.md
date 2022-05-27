# What is OceanBook?

OceanBook aims to deliver a fully on-chain FIFO matching engine, which is gas finite and optimized to be fully viable on the L1 Ethereum Mainnet.

​
To fully understand what PoolSharks team proposes here, we have to understand the markets, how a Queued Market Maker works, and what are the tradeoffs versus an Automated Market Maker.

After we're aware of the Risks and Rewards of being exposed to market making (as a Liquidity Provider), we can start to comprehend where OceanBook really shines.

# Test sections
=== "Layers"
    | Module Name   | Short Description | Status |
    | ------------- | ----------------- | ------ |
    | Core          | Handles the core functionality of tokens, handles basic user token management | Authorized |
    | PredaDex      | Provides a fast way for a user to perform a swap on a given list of DEXes | Development |
    | Group Swap    | Provides a way for multiple users to perform a common swap, reduces gas spent per user | Development |
    | Order Book    | Provides a cheap way for users to have Peer-2-Peer swaps, offers a way for non-DCEX users to also interact with the liquidity inside | Development |
    | Aave          | Provides an option for users to perform common actions like deposit, can reduce gas spent per user | Development |

--8<-- "docs/commons/abbreviations.md"