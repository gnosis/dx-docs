# Integration Ideas

Note: We are giving out bounties and ecosystem grants - if you find an idea particularly interesting and it is not part of one of our schemes - feel free to contact us and we can see if it fits our bounty schedule. More information on this will follow in due time.

Please note that some teams are already working on various ideas. We try to update the section on [projects building on top of the DutchX](https://dutchx.readthedocs.io/en/latest/community-resources.html#projects-using-the-dutchx) for you.

### Table of contents

[More defined sample ideas](#more-defined-sample-ideas)

[Smart contracts](#smart-contracts)

[Front-end](#front-end)

[Services](#services)

[Further ideas](#further-ideas)

[Smart Contracts](#smart-contracts)

[Front-ends](#front-ends)

[Services](#services)

[Ideas for financial instruments](#ideas-for-financial-instruments)

[Ideas for larger projects](ideas-for-larger-projects)

[Ideas for documentation](#ideas-for-documentation)

## More defined sample ideas

### Smart contracts

##### 1. “End to end”-participation solution

- On an interface level (the trading platform that allows the user to interact with the DutchX open protocol), the user must sign several transactions
    - Wrapping ETH
    - Paying with OWL (if available)
    - Allowance of token
    - Confirmation of Order
    - Claim and Withdraw

- It would make sense to have a contract where the user can send ETH (specifically for an auction pair) and the contract does everything automatically and even sends back the exchanged funds to the user’s address
- Smart contract must know how much comes from which address and allocate the exchanged token to this one.  
- Must overcome problem that the DutchX contract needs to be requested to do claim and withdraw
- Must overcome gas problem (take fee from user)?
- Must overcome problem that the pre-set gas limit in most applications might be too low to do one transaction up to confirmation of order.

##### 2. An arbitrage bot which can act as a bridge between the DutchX and another exchange and does a transaction atomically (i.e. one transaction that buys on another exchange and takes part with the funding on the DutchX)  

- Arbitrage opportunities exist if there is a price differential on another exchange and on the DutchX
- For example, on Exchange Y, the price for A in units of B is 1.5. Once the auction A-B reaches this price, it is worthwhile to buy B on Exchange Y and use it to bid in the A-B auction on the DutchX.  
- You need to find an exchange with sufficient liquidity and where such an atomic transaction is possible.
- Added complexity: If it is not the same token pair, but another transaction in between i.e. A for B, B for C and C for A.

##### 3. Pooling contract to have USD 10’000 starting the auction

- The rules in the smart contract is such that a listing token pair is done by  
    - i) specifying the NewToken
    - ii) Funding the auction with the equivalent of 10kUSD in ETH
    - iii) setting the price
    - After 6h, the auction will start

- There might not be sufficient interest by just one party to initiate this; hence, the funding could be pooled
- Contract would specify who inputs how much money and then allocates the exchanged funds based on the same percentage  
- Optional but highly recommended: also collecting funds for the bid side and taking part at a prior specified price.

##### 4. Token BuyBacks (and burn?):  

- A token project might have the need to buy back tokens
- The difficulties thereby could be:
    - On which exchange would the project do this?
    - And how would it publicly announce it?
    - Is it binding? How will it be ensured that they stick to this?
    - Oftentimes it’s difficult to move funds between exchanges

- If there is a smart contract that keeps some parameters open (is somewhat customizable), projects could use the DutchX, which is available to anyone without and larger hurdle.
- The project would inject an amount of ETH as a sellVolume and declare that it will take part in the ETH/SpecificToken auction
- The contract would work such that the following parameters would need to be specified:
    - Amount of ETH to be included in the buy back
    - How many auctions
    - Which specific auctions (by index) and how much in each auction
    - Amount would need to be pre-submitted

- A sample of a buy-and-burn need could be this one: https://research.aragon.org/t/thoughts-on-aragon-network-treasury-governance-and-reserves/180

### Front-end

- Provision of a widget that does data analytics specifically tailored to the need of a seller active on. Two samples of trading interfaces built on top of the DutchX smart contracts are [https://eazy.exchange/](https://eazy.exchange/) and [https://dutchx-rinkeby.d.exchange/](https://dutchx-rinkeby.d.exchange/)
    - Data analytics may include but are not limited to:
        - ETH to EUR/USD price feed  
        - Highest volume auctions
        - Fees part of the sellVolume
        - Last available price overview
        - Countdown for next auction to start (approximation only)

### Services

- A bot that automates listing a token to the back-end.  
    -  The rules in the smart contract is such that a listing token pair is done by  
        - specifying the NewToken
        - Funding the auction with the equivalent of 10kUSD in ETH
        - setting the price for ETH/NewToken
        - After 6h, the auction will start

    - A token project might not want to do this. The bot (or alternatively together with a simple interface) would therefore receive the funding and ask for the price input (both needed to start the auction)
    - Added feature: Bot could take part on the buy side as well as this should really be ensured for triggering the auction. In that case, naturally, the bot would need the bidToken in funding as well.  
    - Added feature: the bot could take the price feed from another exchange rather than asking for it (if a price feed is available).

## Further ideas

### Smart Contracts

- Imitating limit order buy having a contract that is funded by the user and buys back at a certain price (floor)
- Contract that takes out data information from the DutchX - more concrete and historic data.
- Creating a price feed out of it to be used in another instance → build a bridge into another projects (sample project for this: [https://github.com/gnosis/dx-examples-dev/tree/master/03_onchain-usage-oracle](https://github.com/gnosis/dx-examples-dev/tree/master/03_onchain-usage-oracle))
- Arbitrage strategies may differ:
    - Funds are needed to match the order first and buy back (or first on the DutchX)
    - The token swap is such that the order may be settled on behalf of the user (without needing to put up the funds)
        - User needs to set allowance with other exchange and DutchX. Ideally contract would also then cancel the other order on the other exchange.

    - Might be an integration into e.g. 0x.

### Front-ends

- Anything that is a graphical display/widgets. Check out some samples here: [https://www.tradingview.com/widget/](https://www.tradingview.com/widget/)
- Interface to start the listing process
- Deposit and withdraw widget (incl. wrapping and unwrapping ETH)  
    - Currently only deposit and postOrder is done in one and also claim and withdraw.  

### Services

- Email (or bot) notification service when an address has claimable funds
    - User enters to this website
    - User enters email address and wallet address
    - "I would like to be notified if there are claimable funds available in connection with this wallet address" (submit)
    - First time user receives email to confirm email address and privacy policy (if applicable)
    - User has the option to unsubscribe

- Notification bot when a token pair reaches a certain price
- Arbitrage bot between the two opposite auctions

### Ideas for financial instruments

- Decentralized token lending protocol (uses price feed of DutchX and liquidates using the DutchX if collateral falls below a certain amount (proposals have already been handed in)
- A “top 10”-token Fund on the DutchX. Always invests 10% into each of the 10 highest priced tokens. Those token fund tokens can be purchase via the DutchX also

### Ideas for larger projects

- Interface for a bidder participation
- A widget for integration on any project’s website that goes through the DutchX process
    - “Buy ABC”
    - Includes participation in the DutchX as a seller (using ETH)
    - Ideally built on top of the “end-to-end”-solution mentioned above

### Ideas for documentation

- Screencast on CLI participation
- Screencast on participation directly on smart contract level
- Screencast on API
- Screencast on using the minimal liquidity bots
