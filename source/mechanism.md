# Decentralized trading protocol for ERC20 tokens

The DutchX has two phases (for each token pair):<br/>
(1) the batching before an auction starts (for sellers to deposit their tokens)<br/>
(2) and the running Dutch auction (when bidders are active).

Sellers can submit the tokens they would like to sell at any point in time. These tokens will automatically be placed into the next available auction as no tokens can be submitted into the running auction.  

Bidders are only active during the running of an auction.  

There is always only one auction per token pair running (with opposite auctions running simultaneously). All auctions run independent of one another.<br/>  
When an auction for a given token pair begins, the initial price is set at twice the final closing price of the previous auction (of the same pairing). From this initial price, the price falls according to a decreasing function. During the auction bidders can submit their bid at any point in time at that current price (remember: the price function is decreasing). The bidders are guaranteed the minimum amount of tokens at the price point at which they took part. Bidders can submit bids until the auction closes (where bidVolume x price = sellVolume). Note that all bidders receive the same final and therefore lowest price. Bidders should therefore take part where the current price of the auction reflects their maximum willingness to pay.
Since bidders will only pay the final market clearing price, which is either at their bid or lower, they have an economic incentive to submit the bid at their highest willingness to pay.

Check the section on [**interfaces**](https://dutchx.readthedocs.io/en/latest/interfaces.html) for ways to participate.  

## Liquidity contribution
On the DutchX Protocol, liquidity contribution is levied on users in place of traditional fees.<br/>
**These do not go to anyone** (not to Gnosis, or any other party):<br/>
Rather, the liquidity contribution is committed to the next running auction for the respective auction pair and are thus *redistributed to all users of the DutchX protocol*! This mechanism helps boost volume and use of the protocol.<br/>

Your individual liqudity contribution depends on your amount of Magnolia token held as a percentage of the entire Magnolia market (it is a step function):<br/>  
=>10% of Magnolia held --> 0.1% liquidity contribution<br/>  
1%-10% of Magnolia held --> 0.2% of liquidity contribution<br/>  
0.1%-1% of Magnolia held --> 0.3% of liquidity contribution<br/>   
0.01%-0.1% of Magnolia held --> 0.4% of liquidity contribution<br/>  
anything below 0.01% of Magnolia held --> 0.5% of liquidity contribution.  

 **The liquidity contribution could also be positive** for a trader that has lower contribution than other traders in the same pair!

## Magnolia
Magnolia (MGN) tokens are intrinsic to the DutchX and lower the default liquidity contribution on the DutchX Protocol.<br/>  
MGN are automatically generated and credited to users: 1 MGN is credited for trading 1 ETH worth of any whitelisted token pair (and of course trading any fraction of ETH generates the same fraction of MGN).<br/>
MGN are locked by default into a smart contract for which the user’s address is associated with a particular balance.<br/>  
A user may unlock all Magnolia associated with an address at once and after 24 hours have passed, these tokens may be transferred to another address. The new holder must then lock their tokens again (or a portion thereof) in order to use the Magnolia balance for liquidity contribution reduction.<br/>  
Magnolia are inflationary, which should incentivise early adoption and continuous use of the DutchX protocol.<br/>  
Magnolia are not needed to participate as a seller or bidder on the DutchX.

## Whitelist
Whitelisted tokens are tokens that generate Magnolia when traded in a whitelisted pair. Non-whitelisted tokens can still be traded (if added to the DutchX protocol), but will not generate Magnolia! The idea of whitelisted tokens is to maintain MGN's benefit: no token should be traded with the sole intention to create Magnolia and benefit from liquidity contributions (and others' liquidity contribution to be hence reduced).<br/>
Whitelisting is - as per 14 July 2019, 12GMT noon - determined by [the dxDAO](https://dutchx.readthedocs.io/en/latest/dxDAO.html).<br/>  
During the Vote Staking Period, Gnosis whitelisted any tokens that were added to the protocol, which had a reasonable pricefeed AND were also part of this [suggested whitelist](https://github.com/gnosis/dx-contracts/blob/master/test/resources/approve-tokens/dxDAO_approved_tokens.js).<br/>  
This suggested list had been put together based on a legal assessment of token characteristics, which suggest that legislation of major jurisdictions regulating securities, financial instruments or similar and/or mandating customer due diligence procedures do not apply to them at this point in time for the purposes of the DutchX protocol.<br/>
Regardless of being whitelisted, tokens will still first need to be added to the protocol before trading is possible.  

Note that whitelisted tokens are not the same as **listed** and **traded** tokens. A whitelisted token has the potential to create Magnolia tokens (used for reduction of liquidity contribution) if traded in a whitelisted pair. Tokens can be listed for trading on the DutchX protocol, albeit not whitelisted (and hence trades do not generate Magnolia); on the flip side, tokens could in the future also be whitelisted by the dxDAO, however not listed/traded on the DutchX protocol.

- **Check out [this API endpoint](https://dutchx.d.exchange/api/docs/#!/Markets_and_supported_tokens/getWhitelistedTokens) on actually whitelisted tokens.**<br/>
- **Check out [this API endpoint](https://dutchx.d.exchange/api/docs/#!/Markets_and_supported_tokens/getTokens) on added tokens to the DutchX protocol.**

## GNO
There is no special use case for GNO. It is treated as any other ERC20 token.

## OWL
In version DutchX 2.0, OWL is part of the DutchX Protocol:

### What is OWL?
- OWL is an ERC20 token. Check it out on [Etherscan](https://etherscan.io/token/0x1a5f9352af8af974bfc03399e3767df6370d82e4).
- Read this [blog post](https://blog.gnosis.pm/owl-token-use-cases-6094027ecb37) on all the various use cases.

### What is OWL used for on the DutchX?
- Users *may* use OWL to settle half of their liquidity contribution. The rest is settled in the token they are taking part in.
- This does not affect the reduction of your liquidity contribution. The reduction happens first, *then* half may be settled in OWL.
- 1 OWL is treated as an equivalent of 1USD worth of fees.
- The OWL used will not go to **any party** but will instead be burnt (consumed).   

*An example:<br/>
1) user takes part with 100A, where A is any ERC-20 token listed on the DutchX<br/>
2) liquidity contribution is calculated, e.g. 0.3%<br/> 
3) total fees are 0.3A<br/>
4) user chooses to settle half in OWL<br/>
5) calculation of 0.3A into ETH then into USD (e.g. 0.6USD)<br/>
6) 0.3 OWL is deducted (1USD = 1OWL)<br/>
7) remainder of 0.3USD (=0.15 A) is taken from the order<br/>
8) 99.85A is placed for the user as his/her order. Note that 0.3OWL are burnt and 0.15A go into the next auction as an extra sellVolume*

### How is it used on the DutchX?
- OWL is completely optional to use. You must set an allowance for the smart contract for OWL.
- OWL is then deducted automatically (available using the same address you are trading from).
- OWL are, however, not needed to participate as a seller or bidder on the DutchX; its use is completely voluntary.

### Why would one want to use OWL?
- You might have OWL as you used your GNO to generate it.
- You might be able to acquire it for less than 1USD worth and would hence reduce your liquidity contribution!

### How does one get OWL?
- OWL is generated by locking GNO (of course you get the GNO back) during special generation times. 
- Check [this website](https://owl.gnosis.io/) to see if there is an ongoing generation or to see past generations and claim back your GNO if you haven't done so already.
- OWL may be traded on secondary markets or OTC.

## Auctioneer Powers

### What are auctioneer powers?
On smart contract level, the DutchX has a number of clearly defined modifiable parameters that can be changed. The auctioneer has the powers over the following (complete list):

- De- & whitelisting of tokens that generate Magnolia
- Changing the threshold to start auctions
- Changing the threshold to add tokens to the DutchX protocol
- Setting a new external ETH/USD price feed
- Updating the DutchX contract logic, and
- Setting a new entity able to modify the contract parameters (the ‘auctioneer’).

### Why are auctioneer powers needed?
The DutchX was designed to be a fully-decentralized trading protocol. This means that changes to the DutchX protocol must also be decided in a decentralized fashion.  

Specifically, however, there are two reasons that make upgrade by hard-forks only (the alternative to an owner) not very user friendly:
1) Some parameters need more frequent updating (such as the whitelisting mentioned)
2) One of the value propositions of the DutchX is to be one global liquidity pool. If there was not a possibility to upgrade the master logic, one would risk splitting liquidity with every upgrade.

### Who holds auctioneer powers to DutchX 1.0?
In the first version of the DutchX smart contracts, these auctioneer powers were relinquished. This meant that **neither Gnosis nor anyone else**, had the ability to alter the contracts parameters or logic.

### Who holds auctioneer powers to DutchX 2.0?
The primary aim with this deployment was to provide the [dxDAO](https://dutchx.readthedocs.io/en/latest/dxDAO.html) with the auctioneer powers of the DutchX. The following parameters may be modified by successful proposal in the dxDAO.

### Some more details to the auctioneer powers:
#### De- & whitelisting of tokens that generate Magnolia
TODO
#### Changing the threshold to start auctions
TODO
#### Changing the threshold to add tokens to the DutchX protocol
TODO
#### Setting a new external ETH/USD price feed 
TODO*(change only executed with a 30day time lag)*
#### Updating the DutchX contract logic 
TODO*(change only executed with a 30day time lag)*.
#### Setting a new auctioneer
TODO
