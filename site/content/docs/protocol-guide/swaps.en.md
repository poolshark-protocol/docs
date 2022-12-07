# Swaps

![Screenshot](swap-icon.png){: .center style="height:200px; width:200px;"}

### How is a swap executed?

- Taker chooses token pair to perform swap
- Taker requests swap transaction
- Liquidity is aggregated from several `Concentrated Liquidity Positions` and respective ticks
- Order is filled according to the average price quote from said ticks
- Liquidity gets taken from all LPs/makers according to how tight their liquidity range is (e.g. tighter liquidity ranges will be prioritized for providing liquidity for the swap)
- Individual end LPs/makers that provided liquidity for the given swap get fees according to their selected `Fee Tier`

<br/>
<br/>
<br/>
