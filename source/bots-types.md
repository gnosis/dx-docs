# DutchX Bots
When we start the application, it will start also 3 bots.

Every bot is created with one goal, so once they are up, the will try to do
their jobs.

## Sell Liquidity Bot
> This bot requires WATCH_EVENTS_BOT to be configured and tracking the same MARKETS

This bot will make sure we meet the minimum liquidity required
by the smart contract for the auction to start.

In other words, it makes sure the auction starts automatically filling the
missing sell volume.

The smart contract won't start the auction, unless we have more than
`$1.000` worth of the sell token, so this bot fill the missing difference.

**When will this bot ensure the sell liquidity?**

It will ensure it as soon as both of the opposite auctions clear for a token pair.

**Which of the two auctions it will fund?**

It will fund the one with the highest funding, so it has to fill with less worth
of tokens.

### Sell Liquidity Bot configuration
* `SELL_BOT_MAIN`:
  * **name**: The name to display in notifications and messages
  * **factory**: The factory to create the bot. You can create your own bot if you want!
  * **markets**: An object selecting the markets to watch (as explained [here](./bots-market-making.html#create-the-config-file-for-the-bots))
  * **accountIndex**: The accountIndex from the accounts generated from the `MNEMONIC` that is going to be used by this bot
  * **notifications**: The notification system to be used by the bot. For now only `slack` is available
  * **checkTimeInMilliseconds**: the time between bot checking to sell liquidity  

## Buy Liquidity Bot
This bot will make sure the auction closes when we reach the market price.

If nobody bids when the auction is on the market price, the price will continue
to go down, and eventually, after 24h, could get to 0.

To avoid this situation, the buy bot will buy automatically when the token price
is at a right price.

**How does the bot know what is the market price?**

Right now the buy bot can check in any of these exchanges:

* **Binance**: https://www.binance.com
* **Bitfinex**: https://www.bitfinex.com/
* **HitBTC**: https://hitbtc.com/
* **Huobi**: https://www.huobi.com
* **IDEX**: https://idex.market/
* **Kraken**: http://kraken.com
* **Liquid**: https://www.liquid.com/

Depending on the token pair, we can configure an strategy for getting the
market price.

If you consider that none of these exchanges fits to your needs you can make a
pull request and add a new one. Check here
[how to add a price feed](https://dutchx.readthedocs.io/en/latest/bots-price-feed.html)

### Buy Liquidity Bot configuration
* `BUY_BOT_MAIN`:
  * **name**: The name to display in notifications and messages
  * **factory**: The factory to create the bot. You can create your own bot if you want!
  * **markets**: An object selecting the markets to watch (as explained [here](./bots-market-making.html#create-the-config-file-for-the-bots))
  * **accountIndex**: The accountIndex from the accounts generated from the `MNEMONIC` that is going to be used by this bot
  * **rules**: The rules to indicate the bot when to do buys (read next section)
  * **notifications**: The notification system to be used by the bot. For now only `slack` is available
  * **checkTimeInMilliseconds**: the time between bot checking to buy liquidity  

### Buy Liquidity Bot price repository
* `PRICE_REPO`:
  * **factory**: The factory to create the repository. You can create your own repository if you want!
  * **priceFeedStrategiesDefault**: The default price feed strategy object (read next section)
  * **priceFeedStrategies**: The price feed strategy object for each token pair (read next section)
  * **priceFeeds**: The price feed factory. You can implement your own
  * **strategies**: The strategies factory. You can create your own

**Strategies for getting the price - Sequence**

The current strategy implemented by the buy bot is called `sequence`, but more
strategies could be implemented for future versions.

For example, we could configure the bots with the following strategies:
```js
priceFeedStrategiesDefault: {
  strategy: 'sequence',
  feeds: ['binance', 'huobi', 'kraken', 'bitfinex']
},

priceFeedStrategies: {
  'WETH-OMG': {
    strategy: 'sequence',
    feeds: ['binance', 'huobi', 'bitfinex']
  },
  'WETH-RDN': {
    strategy: 'sequence',
    feeds: ['huobi', 'binance', 'bitfinex']
  }
}
```

For the `sequence` strategy we can define a sorted list of the exchanges we want
to use for getting the price.

The buy bot will try to get the price from the first exchange, if it's down or
unresponsive, it will try to get the price from the second one, and so on.

The idea is to pick the order using first the most trusted exchanges, for
example we could use the trade volume to help us decide.

You can select other strategies or priceFeeds. First they should be added to the
bots git repository and then you can add them by configuration. Check here [how to add a price feed](https://dutchx.readthedocs.io/en/latest/bots-price-feed.html)
```js
priceFeeds: {
  binance: {
    factory: 'src/repositories/PriceRepo/feeds/PriceRepoBinance'
  },
  kraken: {
    factory: 'src/repositories/PriceRepo/feeds/PriceRepoKraken',
    url: 'https://api.kraken.com',
    version: '0'
  }
},
strategies: {
  sequence: {
    factory: 'src/repositories/PriceRepo/strategies/sequence'
  }
}
```

**Buy liquidity rules**

Another important part of the buy liquidity bot, is the buy rules.

These rules allow the bot to decide how much they should buy, and in what
precise moment.

For example, we could define these rules:
* Ensure that **1/3 of the sell volume** is bought when the **price equals the
market price**.
* Ensure that **2/3 of the sell volume** is bought when the **price is 2% below
the market price**.
* Ensure that **the whole sell volume** is bought when the **price is 4% below
the market price**.

This rules can be specified using this configuration:

```js
const BUY_LIQUIDITY_RULES = [
  // Buy 1/3 if price equals market price
  {
    marketPriceRatio: {
      numerator: 1,
      denominator: 1
    },
    buyRatio: {
      numerator: 1,
      denominator: 3
    }
  },

  // Buy 2/3 if price falls below 98%
  {
    marketPriceRatio: {
      numerator: 98,
      denominator: 100
    },
    buyRatio: {
      numerator: 2,
      denominator: 3
    }
  },

  // Buy the 100% if price falls below 96%
  {
    marketPriceRatio: {
      numerator: 96,
      denominator: 100
    },
    buyRatio: {
      numerator: 1,
      denominator: 1
    }
  }
]
```

## Balance Check Bot
The liquidity bots are very useful, but in order to operate, they need to have
enough tokens to perform the bids and asks, and also some Ether so they can
pay the gas costs for the transactions.

This bot will check periodically the balances for the bots and will show a
warning message when we are below the defined threshold.

> In the future, we will provide a way to send the notification using Slack or
> mail.

### Balance Check Bot configuration
* `BALANCE_CHECK_BOT`:
  * **name**: The name to display in notifications and messages
  * **factory**: The factory to create the bot. You can create your own bot if you want!
  * **tokens**: A list selecting the desired tokens to follow (ex. ['WETH', 'RDN'])
  * **accountIndex**: The accountIndex from the accounts generated from the `MNEMONIC` that is going to be used by this bot
  * **notifications**: The notification system to be used by the bot. For now only `slack` is available
  * **minimumAmountForEther**: the minimum amount of Ether we want the bot to hold
  * **minimumAmountInUsdForToken**: the minimum amount of any other token in USD

**Balance thresholds**

For example, the rules could be, notify if we are below:
* `0.4 Ether`
* `$5000` worth of any tokens

So we would have this configuration:
```js
minimumAmountForEther: 0.4, // 0.4 Ether
minimumAmountInUsdForToken: 5000 // $5000
````

## High Sell Volume Bot
This bot will check the markets you select and will send a log notification if
any of the markets volume is over your account balance. This is very handful if
you want to ensure liquidity to a market and want to make sure that all liquidity
is bought.

### High Sell Volume Bot configuration
* `HIGH_SELL_VOLUME_BOT`:
  * **name**: The name to display in notifications and messages
  * **factory**: The factory to create the bot. You can create your own bot if you want!
  * **markets**: An object selecting the markets to watch (as explained [here](./bots-market-making.html#create-the-config-file-for-the-bots))
  * **accountIndex**: The accountIndex from the accounts generated from the `MNEMONIC` that is going to be used by this bot
  * **notifications**: The notification system to be used by the bot. For now only `slack` is available


## Deposit Bot
This bot will check periodically your account balances and will automatically
deposit tokens into the DutchX. This is very handful when a bot is running out
of funding. You just have to send the tokens to the bot account and the deposit
bot will handle the rest.

### Deposit Bot configuration
* `DEPOSIT_BOT`:
  * **name**: The name to display in notifications and messages
  * **factory**: The factory to create the bot. You can create your own bot if you want!
  * **tokens**: A list selecting the desired tokens to follow and deposit (ex. ['WETH', 'RDN'])
  * **accountIndex**: The accountIndex from the accounts generated from the `MNEMONIC` that is going to be used by this bot
  * **notifications**: The notification system to be used by the bot. For now only `slack` is available
  * **inactivityPeriods**: a list of from-to time periods in which the bot will not deposit funds (useful when you want to withdraw)
  * **checkTimeInMilliseconds**: the time between bot checking to deposit funds  

## Claim Bot
This bot will check periodically for unclaimed balances in the configured markets
and will automatically claim all of them. This is useful so the bot can recover
on his own funds used on previous auctions.

### Claim Bot configuration
* `CLAIM_BOT`:
  * **name**: The name to display in notifications and messages
  * **factory**: The factory to create the bot. You can create your own bot if you want!
  * **markets**: An object selecting the markets to watch (as explained [here](./bots-market-making.html#create-the-config-file-for-the-bots))
  * **accountIndex**: The accountIndex from the accounts generated from the `MNEMONIC` that is going to be used by this bot
  * **notifications**: The notification system to be used by the bot. For now only `slack` is available
  * **autoClaimAuctions**: the number of previous auctions you want the bot to check (ex. 90 will correspond to aprox 3 weeks of auctions if around 4 auctions each day)
  * **cronSchedule**: You can select using crontab style a time schedule for the claim. You can check [here](https://crontab.guru/#0_02,06,10,14,18,22_*_*_*) if you have doubts.

## Watch Events Bot
This bot can watch for events in market auctions to operate immediately once an auction
has closed.

* `WATCH_EVENTS_BOT`:
  * **name**: The name to display in notifications and messages
  * **factory**: The factory to create the bot. You can create your own bot if you want!
  * **markets**: An object selecting the markets to watch (as explained [here](./bots-market-making.html#create-the-config-file-for-the-bots))
