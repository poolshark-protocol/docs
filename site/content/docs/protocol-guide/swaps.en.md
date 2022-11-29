# Swaps

![Screenshot](swap-icon.png){: .center style="height:200px; width:200px;"}

### How is a swap executed?

- Taker chooses token pair to perform swap
- Taker requests swap transaction
- `Poolshark` is parsed through the router to check if there's an adequate ask for the corresponding bid or vice-versa
- If the order is not fully filled by then, liquidity is aggregated from several `Concentrated Liquidity Positions` and respective ticks
- Order is filled according to the average price quote from said ticks
- Output fees are distributed to all LPs/makers according to how tight their liquidity range is (e.g. tighter liquidity ranges will be prioritized for providing liquidity for the swap and will have bigger aggregated fee accrual from said swap), so the individual end LPs/makers that provided liquidity for the given swap get fees according to their selected `Fee Tier` when opening a `Concentrated Liquidity Position`

<br/>
<br/>
<br/>
