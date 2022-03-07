# Modules

The DCEX design supports modularity, this table lists all the modules
=== "Layers"
    | Module Name   | Short Description | Status |
    | ------------- | ----------------- | ------ |
    | Core          | Handles the core functionality of tokens, handles basic user token management | Authorized |
    | Quick Swap    | Provides a fast way for a user to perform a transfer on a given list of DEXes | Development |
    | Group Swap    | Provides a way for multiple users to perform a common swap, reduces gas spent per user | Development |
    | Order Book    | Provides a cheap way for users to have Peer-2-Peer swaps, offers a way for non-DCEX users to also interact with the liquidity inside | Development |
    | Aave          | Provides an option for users to perform common actions like deposit, can reduce gas spent per user | Development |

--8<-- "docs/commons/abbreviations.md"