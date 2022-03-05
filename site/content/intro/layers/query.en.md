# Database Query

## What It Does

The query layer resolves the trustless interactions between the Execution Layer (Gelato Network) and the Data Layer (The Graph Network) and ensures data has been properly validated prior to initiating any transactions on-chain. This layer is still under heavy construction and is the primary blocker for creating a fully trustless execution loop comprised of on-chain and off-chain components. 

???+ example
    ```mermaid
    graph LR
        A[User] -->|API Call| B{{Query Layer}};
        B -->|Query Subgraph| C[Decentralized Node Query];
        C -->|valid zkSnark?| D[return response];
        C -->|invalid zkSnark?| E[Submit Dispute];
        E -->|Retry| B;
    ```

## Abstraction

The Query Layer abstracts away receiving trustless data from The Graph decentralized network back on-chain in the form of withdraws, swaps, and other on-chain settlement which are executed on the Gelato Network.

## User Functionality

Users looking to engage in the following areas can utilize the Query Layer to receive trustless data: MEV, predictions, analytics, monitoring, etc. These are just a few examples of users that might have a financial or data-driven incentive to query The Graph Network. We believe bringing a financial use case to data networks will help them flourish in the long-run.

If you believe you have a decentralized network where we can host our API for validating data from The Graph, please reach out to us via Twitter or Discord.

## Production Requirements

Trustless data is an absolute requirement in creating a non-custodial trustless exchange where users can coordinate on-chain actions together.

Likely we will have to build out our own data validation layer in an effort to dispute either data that is indexed incorrectly or query results that are found to be invalid. This will effectively slash bad actors on The Graph Network and prevent our Execution Layer from acting on invalid data.
--8<-- "docs/commons/abbreviations.md"