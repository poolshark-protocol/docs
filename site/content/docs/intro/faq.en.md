### **How does the OceanBook protocol compare to a traditional centralized exchange orderbook?**

In comparison to a centralized exchange orderbook, on-chain limit order books cannot be equally expressive without encountering scalability issues.

This means that each `Book` contract will support limited precision with respect to the possible exchange rates between tokens.

The goal is to strictly limit the amount of on-chain storage access in order to maximize volume for the benefit of everyone.

In order to achieve this we must maximize deterministic behavior.

Traditionally this is why AMMs have worked quite well, and the same rules apply here.

This means accomodating for trades of different sizes separately as the amount of data each of these will load can be drastically different.

More details on how we solved for this will be released alongside the launch of public testnet.

<br/>
<br/>