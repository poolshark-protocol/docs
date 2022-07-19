# QMM Core Concepts

Queued Market Makers differ from other decentralized exchange models in that they have a split buy and sell side.

Each `Book` contract is composed of the following:

- Two lists of `Pages`
    - one for each trading direction
- A set of `Orders`
    - each order is mapped to a `Page`

A `Page` is a `Fungible Queue` which contains the following items:
```
    - Price
        - This is used to determine exchange rate between `Makers` and `Takers`

    - Volume counter
        - In the smart contracts, this will be referred to as `currentOffset`
        - This is used to track which `Maker` orders have been filled
        - When `Makers` go to claim and/or replace their order,
          this value will be checked
            - Example: `currentOffset` is halfway between `start` and `end`
                       of `Maker` order and therefore 50% of their order will
                       be claimable along with fees.

    - Next page
        - The identifier for the next lowest-priced page
        
    - Previous page
        - The identifier for the previous lowest-priced page

    - Cancel list
        - Cancels function as someone stepping out of the queue
        - These are checked for on each `Taker` order
        - More details on how these are handled will be released upon
          public testnet launch
        - Current estimated costs is 31,000 gas + ERC20 transfer cost


```
<br/>
<br/>