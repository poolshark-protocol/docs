---
title: Introduction
some_url: https://github.com/daifoundation/maker-otc
---
># **What is Poolshark?**

The Poolshark Protocol is a set of smart contracts which introduces **Directional Liquidity** into the world of decentralized exchanges.

It has elements of a traditional `Range AMM` (e.g. Uniswap v3), where LPs are free to choose a range in which to allocate their capital.

Liquidity Positions are then aggregated together into a single pool for users to trade against.

With Directional Liquidity, users can 

1. Choose the trade direction
2. Protect against adverse price movements
3. Offer better prices than other pools

## **Choose the Trade Direction**

In a traditional liquidity pool, LP postiions trade both directions.


```python
import plotly.graph_objects as go

import numpy as np

# Generate curve data
t = np.linspace(-1, 1, 100)
x = t + t ** 2
y = t - t ** 2
xm = np.min(x) - 1.5
xM = np.max(x) + 1.5
ym = np.min(y) - 1.5
yM = np.max(y) + 1.5
N = 50
s = np.linspace(-1, 1, N)
xx = s + s ** 2
yy = s - s ** 2


# Create figure
fig = go.Figure(
    data=[go.Scatter(x=x, y=y,
                     mode="lines",
                     line=dict(width=2, color="blue")),
          go.Scatter(x=x, y=y,
                     mode="lines",
                     line=dict(width=2, color="blue"))],
    layout=go.Layout(
        xaxis=dict(range=[xm, xM], autorange=False, zeroline=False),
        yaxis=dict(range=[ym, yM], autorange=False, zeroline=False),
        title_text="Kinematic Generation of a Planar Curve", hovermode="closest",
        updatemenus=[dict(type="buttons",
                          buttons=[dict(label="Play",
                                        method="animate",
                                        args=[None])])]),
    frames=[go.Frame(
        data=[go.Scatter(
            x=[xx[k]],
            y=[yy[k]],
            mode="markers",
            marker=dict(color="red", size=10))])

        for k in range(N)]
)

fig.show()
```

<br/><br/>
![Screenshot](book_screenshot.png){: .center style=""}
<br/>

With these added features, liquidity providers can customize their risk profile to match the current price action in the market.

<em>Directional LPing</em> allows for one-way fills similar to a traditional limit order, whereas current LP positions will trade both ways.

<br/><br/>








