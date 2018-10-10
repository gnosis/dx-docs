# Add a price feed
Although there are some price feeds implemented on the bots they may not be enough
for your needs. Whether your token is not listed in any of them, or they don't have
enough volume in order to use them as trusty price feed, you can add the one that
fits to your needs and create a pull request to the project for being able to use it.

## 1. Fork dx-services project
Bots are implemented in the
[DutchX Services](https://github.com/gnosis/dx-services) project and are Open
Source for anyone to use, modify, or improve.

For this case you should fork this project, using `develop` branch

## 2. Adding the new price feed repository
The price repository is implemented in
[src/repositories/priceRepo](https://github.com/gnosis/dx-services/tree/develop/src/repositories/PriceRepo)
In this folder you can find another two folders:
* feeds - here is where we add integrations with price feeds
* strategies - here we add the logic of strategies used to check the price

We need to add a new feed in the `feeds` folder. You can check other integrations
or use them as a template in order to speedup your task.

The feed should expose a `getPrice` function. You can check [this example]
(https://github.com/gnosis/dx-services/blob/85439c3d80481e3f0c321ebfc12c2676c1463b5f/src/repositories/PriceRepo/feeds/PriceRepoBinance.js#L37)
This function should return the current price of the token pair.

If you check on another feeds you will also notice a `getSymbols` function,
which is very useful for checking that the queried token pair exists at the external
provider. Usually this function also determines if the given token order is correct,
as many external providers will only accept token pair query in a precise order.
We have also implemented a Cache system for the `getSymbols` function that you should
use in order to avoid repeating lot of heavy queries, as the symbols get updated very rarely.
You can check [this example] for `getSymbols` function
(https://github.com/gnosis/dx-services/blob/85439c3d80481e3f0c321ebfc12c2676c1463b5f/src/repositories/PriceRepo/feeds/PriceRepoBinance.js#L16)

## 3. While adding the price feed
You can use our playground to see if your integration is returning the expected
values.
[ExchangePriceRepo playground](https://github.com/gnosis/dx-services/blob/develop/tests/playground/ExchangePriceRepo/getPrice.js)
You may change the configuration, run this file with
`node tests/playground/ExchangePriceRepo/getPrice.js` and check if your integration is
returning the price values or some error

## 4. Unit testing the price repository
Adding testing is a very good practice when programming. In this case can help us
detecting changes of the API system used to create the feed. This way it's easier
to prevent you failing to get a price by a non reachable external provider.

You can find some automated unit testing in
[tests/repositories/ExchangePriceRepo](https://github.com/gnosis/dx-services/tree/develop/tests/repositories/ExchangePriceRepo)
You can add the unit testing for your feed in this folder and, as before, don't
hesitate to use one of the already existing ones to speed up your task.

## 5. Add a Pull Request to our repository
Once you are comfortable with your integration you should upload your changes to
Github and open a Pull Request to `develop` branch on
[DutchX Services](https://github.com/gnosis/dx-services).
We will review your code and merge it to our repository if everything is correct.

## 6. Thank you for your collaboration
Thank you so much for your collaboration!!
