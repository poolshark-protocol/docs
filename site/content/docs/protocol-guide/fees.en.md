# Fees

The fee system for the protocol is based on static fee tiers. Fee priority is based on how tight the range for a `Concentrated Liquidity Position` is. The individual LP fee accrual after a swap is attributed based on these two parameters. Fee tiers are expressed in `Basis Points` (e.g. 1 `Basis Point` represents 1/100 of 1%, or 0.01% of the used liquidity for a given swap). When creating a new position the LP/maker will be able to choose between one of the following fee tiers:

### Current Fee Tiers

- 1 `Basis Point`
- 5 `Basis Points`
- 10 `Basis Points`
- 100 `Basis Points`
<br/>
<br/>
<br/>
