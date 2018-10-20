# Run your own bots on the DutchX
Bots are series of small applications that run in the background and have a
scoped task to fulfill.

They interact with the DutchX performing some operations.

For example, **liquidity bots** watch some markets and provide liquidity to ensure
that auctions run continuously and prices don't drop below the market price.

Running bots is important for markets where there's insufficient volume or a
market maker in place.

![Bots cycle](./_static/bots-cycle.png)

Bots are implemented in the
[DutchX Services](https://github.com/gnosis/dx-services) project and are Open
Source for anyone to use, modify, or improve.

## Run your own bots
To run your own bots, follow the steps in the guide:
* [https://github.com/gnosis/dx-examples-liquidity-bots](https://github.com/gnosis/dx-examples-liquidity-bots)

## Next steps
You may be also interested in:
* [Add a price feed for your bots](./bots-price-feed.html)
* [DutchX as an open protocol](./dutchx-as-an-open-protocol.html)
* [Add a token pair](./add-token-pair.html)
* [API](./api.html)
* [CLI](./cli.html)
