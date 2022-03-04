# Database Query

## What It Does

The query layer resolves the trustless interactions between the Execution Layer (Gelato Network) and the Data Layer (The Graph Network) and ensures data has been properly validated prior to initiating any transactions on-chain. This layer is still under heavy construction and is the primary blocker for creating a fully trustless execution loop back on-chain. 

## Abstraction

The Query Layer abstracts away receiving trustless data from The Graph decentralized network back on-chain in the form of withdraws, swaps, and other on-chain settlement which are executed on the Gelato Network.

## User Functionality

Users looking to engage in the following areas can utilize the Query Layer to receive trustless data: MEV, predictions, analytics, monitoring. These are just a few examples of users that might have a financial or data-driven incentive to query The Graph Network. We believe bringing a financial use case to data networks will help them flourish in the long-run.

If you believe you have a decentralized network where our use case can fit in around data consensus, please reach out to us via Twitter or Discord.

## Production Requirements

Trustless data is an absolute requirement in creating a non-custodial trustless exchange where users can coordiante on-chain actions together.

Likely we will have to build out our own data validation layer so data that is found to be falsified, either queries or indexing of data, can be disputed. This will effectively slash bad actors in The Graph Network and prevent our Execution Layer from acting on invalid data.
--8<-- "docs/commons/abbreviations.md"