# Buy Bot price feed
If you are running the bots it's important to have a good price feed for the
token pair you are trading.

The **Buy Bot** can be configured to follow some rules. For example:
* Buy `33%` of the sell volume if we are 1% below the market price
* Buy `66%` if we are 2% below the market price
* Buy `100%` if we are 4% below the market price

The thing is, **how does the bot know what is the market price?**

In the bot configuration, the market will be associated with a list of
price feeds (exchanges that report the current price):
* https://github.com/gnosis/dx-examples-liquidity-bots/blob/master/conf/bots.js#L73

Every market can have it's own feed list, and can be configured to use them
following a strategy. At least one price feed is necessary.

## Price Feed
There are many price feeds already implemented, for example:
* **Binance**: https://www.binance.com
* **Bitfinex**: https://www.bitfinex.com/
* **HitBTC**: https://hitbtc.com/
* **Huobi**: https://www.huobi.com
* **Kraken**: http://kraken.com
* **Liquid**: https://www.liquid.com/

You can use any price feed available here:
https://github.com/gnosis/dx-services/tree/master/src/repositories/PriceRepo/feeds

The next section will show you how to add a new price feed.

## Add your own Price Feed
You can use any price feed available here:
https://github.com/gnosis/dx-services/tree/master/src/repositories/PriceRepo/feeds

If the one that you need is missing, you can implement it on your own and
create a `Pull Request` so it can be added to the project.

To implement a new price feed, is as simple as create a new Javascript file
that implement the function:

```js
+ getPrice ({ tokenA: String, tokenB: String }) : Promise<Number>
```

## 1. Fork dx-services project
Bots are implemented in the
[DutchX Services](https://github.com/gnosis/dx-services) project and are Open
Source for anyone to use, modify, or improve.

You should fork this project, using `develop` branch.

## 2. Add the new price feed repository
The price repository is implemented in
[src/repositories/priceRepo](https://github.com/gnosis/dx-services/tree/develop/src/repositories/PriceRepo)
In this folder you can find another two folders:
* **feeds**:
  * Price feeds implementations
* **strategies**:
  * Strategies used to check the price.
  * Right now only `sequence` strategy is implemented.
  * This strategy will be configured with a list of price feeds
  * The strategy will try to get the price from the first feed, if the price is
    not available (i.e. the exchange API service is down), it'll try with the
    second feed in the list, and so forth.
  * It's OK to have just one feed in your list, but keep in mind that if the
    feed is down, the buy bot will wait until is up again.

So,to add a new price feed, we need to add a new implementation to the `feeds`
folder.

You can check other integrations or use them as a template in order to speedup
your task.

Your new implementation should expose the following method:

```js
+ getPrice ({ tokenA: String, tokenB: String }) : Promise<Number>
```

This function receives a token pair (i.e. `{ tokenA: 'RDN', tokenB, 'WETH' }`)
and returns a promise with the current price of the token pair.

Check out [this example](https://github.com/gnosis/dx-services/blob/85439c3d80481e3f0c321ebfc12c2676c1463b5f/src/repositories/PriceRepo/feeds/PriceRepoBinance.js#L37):

If you take a look on another feeds you will also notice a `getSymbols` function,
which is very useful for checking that the queried token pair exists at the
external provider.

Usually this function also determines if the given token order is correct,
as many external providers will only accept token pair query in a precise order.

We have also implemented a Cache system for the `getSymbols` function that you
should use in order to avoid repeating lot of heavy queries, as the symbols get
updated very rarely and some exchanges might limit the number of request they
allow you to do.

You can check [this example](https://github.com/gnosis/dx-services/blob/85439c3d80481e3f0c321ebfc12c2676c1463b5f/src/repositories/PriceRepo/feeds/PriceRepoBinance.js#L16) for the `getSymbols` function.

## 3. While adding the price feed
You can use our playground to see if your integration is returning the expected
values.
[ExchangePriceRepo playground](https://github.com/gnosis/dx-services/blob/develop/tests/playground/ExchangePriceRepo/getPrice.js)

You may change the configuration, run this file with
`node tests/playground/ExchangePriceRepo/getPrice.js` and check if your integration is
returning the price values or some error

## 4. Unit testing the price repository
Add also a test for the new price feed.

It'll verify that it works properly and can help to detect possible future
changes of the API your feed implementation rely on.

You can find some automated unit testing in
[tests/repositories/ExchangePriceRepo](https://github.com/gnosis/dx-services/tree/develop/tests/repositories/ExchangePriceRepo)

Add the unit test for your feed in this folder and, as before, use one of the
already existing ones to speed up your task.

## 5. Add a Pull Request to our repository
Once you are comfortable with your integration you should upload your changes to
Github and open a Pull Request to `develop` branch on
[DutchX Services](https://github.com/gnosis/dx-services).

We will review your code and merge it to our repository if everything is correct.

Once merged into `develop`, a new docker image with the changes will be
automatically pushed:
* https://hub.docker.com/r/gnosispm/dx-services/tags/

Periodically, a new stable version is release, so once merged into master, the
changes will be ready in the `staging` version.

## 6. Thank you for your collaboration
Thank you so much for your collaboration!!
