# Swaps

![Screenshot](swap-icon.png){: .center style="height:200px; width:200px;"}

### How is a swap executed?

- Taker chooses token pair to perform swap
- Taker requests swap transaction
- `OceanBook` is parsed through the router to check if there's an adequate ask for the corresponding bid or vice-versa
- If the order is not fully filled by then, liquidity is aggregated from several `Concentrated Liquidity Positions` and respective ticks
- Order is filled according to the average price quote from said ticks
- Output fees are distributed to all LPs/makers according to how tight their liquidity range is (e.g. tighter liquidity ranges will have bigger fee accrual from said swap)

<br/>
<br/>
<br/>