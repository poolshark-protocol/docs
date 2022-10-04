<em>OceanBook has four main components:</em>

1. `Book`
    * an on-chain representation of the liquidity in each `Page` (see core concepts)
2. `Matching engine`
    * the smart contract code to first prioritze price and then time
3. `Router`
    * the means by which maker and taker orders will be sent to the appropriate `Book` contract
4. `Factory`
    * the contract which will launch new OceanBook contracts