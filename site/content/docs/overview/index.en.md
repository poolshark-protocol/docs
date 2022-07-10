# Overview

The OceanBook protocol is a peer-to-peer decentralized exchange which introduces efficient **price time priority** into the world of decentralized exchanges.

It is specifically built for fully fungible ERC-20 token exchange on EVM-compatible blockchains and meant to function as an **on-chain limit order book**.

The protocol will be implemented as a set of non-upgradable smart contracts to enable full permissionless access and to protect against censorship resistance.

The smart contracts for the protocol will be open-sourced upon completion of multiple internal and external audits as well as a public testnet launch.

## How does the OceanBook protocol compare to a traditional centralized exchange orderbook?

In comparison to a centralized exchange orderbook, on-chain limit order books cannot be equally expressive without encountering scalability issues.

This is due to the limitations around how much data can be loaded within a single smart contract transaction.

Thus, one of the core driving principles in the design of the protocol is to maximize deterministic behavior in order to accomodate trades of different sizes.