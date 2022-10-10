# Fees

The fee system for the protocol is based on static fee tiers. The tighter the liquidity range and the less liquid a given pair is, the bigger the final fee revenue for providing said liquidity, and vice-versa. This means that for a given `Concentrated Liquidity Position` the closest/most accurate individual LP fee accrual after a swap is done based on these two parameters. The use of makers' `Concentrated Liquidity` and its consequent attribution of fees will prioritize LPs with tighter ranges for the given swap.  Fee tiers are expressed in `Basis Points` (e.g. 1 `Basis Point` represents 1/100 of 1%, or 0.01% of the used liquidity for a given swap). When creating a new position the LP/maker will be able to choose between one of the following fee tiers:

### Current Fee Tiers

- 1 `Basis Point`
- 5 `Basis Points`
- 10 `Basis Points`
- 100 `Basis Points`
<br/>
<br/>
<br/>
