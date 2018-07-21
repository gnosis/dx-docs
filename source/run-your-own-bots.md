# Run your own bots for DutchX
The bots are series of small applications that run in the background and have a
scoped task to fulfil.

They interact with the DutchX performing some operations.

For example the **liquidity bots** watch some markets and provide liquidity ensuring
the auctions run continuously and the prices don't drop below market price.

Running the bots is important for markets were there's insufficient volume or a
market maker in place.

![Bots cycle](./_static/bots-cycle.png)

The bots are implemented in
[DutchX Services](https://github.com/gnosis/dx-services) project and are Open
Source for anyone to use, modify or improve.

For more information, and details on a easy way on how to run them visit:
* [https://github.com/gnosis/dx-examples-liquidity-bots](https://github.com/gnosis/dx-examples-liquidity-bots)

You may be also interested in:
* [DutchX as an open platform](./dutchx-as-an-open-platform.html)
* [Add a token pair to DutchX](./add-token-pair.html)
