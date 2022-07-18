## Apache Kafka: Scalable Real-Time Data Feeds

To understand the principal motivation behind Fungible Queues and why they work, let's look to message queue architecture from previous generations.

Apache Kafka was created by a team led by Jay Kreps, Jun Rao, and Neha Narkhede at LinkedIn in 2010. Kafka’s architecture was built with the ability to handle billions of individual events in mind with varying sizes.

To understand Apache Kafka Queues we should know the relevant concepts:

- `Topics`
- `Offsets`

![Screenshot](offset.png){: .center style="height:350px; width:900px;"}

In the above figure, a `Topic` is simply a log of events . In our case, each event represents an individual `Order`. Thus, events `1` through `100` can each represent an `Order` each with differing sizes.

A `Topic` here can be equated to a `Page` in each `Book` contract. When you write a new event to the `Topic`, it always goes on the end. Each `Topic` maintains an `Offset` which will always tell which events have already been processed. This allows Kafka to obey the principle of `Exactly-Once Processing`. 

While we only have synchronous processing in the context of a blockchain, this concept of an `Offset` does allow us to tell `Producers`, otherwise known as `Market Makers` in the context of orderbooks, when their `Order` has been filled.

The `Offset` in the context of OceanBook simply plays the role of tracking how much volume has occurred on a given `Page` and relating that to the point where the `Market Maker` pushed their `Order` to the queue.

<br/>
<br/>
<br/>
