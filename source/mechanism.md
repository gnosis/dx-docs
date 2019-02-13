# Decentralized trading protocol for ERC20 tokens

The DutchX switches between two states (for each token pair):  
(1) the batching before an auction starts (for sellers to deposit their tokens), and  
(2) the running Dutch auction (when bidders are active).  

Sellers can submit the tokens they would like to sell at any point in time. Those will automatically be placed into the next available auction — no tokens can be submitted into the running auction.  

Bidders are only active during the running of an auction.  

There is always only one auction per token pair running (with opposite auctions running simultaneously). All auctions run independent of one another.  
When an auction for a token-pairing starts, the initial price is set at twice the final closing price of the previous auction (of the same pairing). From this initial price, the price falls according to a decreasing function. During the auction, when bidders are active, they submit their bid at any point in time at that current price (remember: the price function is decreasing). The bidders are guaranteed the minimum amount of tokens at the price point at which they took part. Bidders can submit bids until the auction closes (where bidVolume x price = sellVolume). Note that all bidders receive the same final and therefore lowest price. Bidders should therefore take part where the current price of the auction reflects their maximum willingness to pay.
Since bidders will only pay the final market clearing price, which is either at their bid or lower, they have an economic incentive to submit the bid at their highest willingness to pay.
  
Check the section on **interfaces** for ways to participate.  
  
## Liquidity contribution
On the DutchX Protocol, liquidity contribution is levied on users in place of traditional fees. 
**These do not go to anyone** (not to Gnosis, or any other party):
Liquidity contribution is committed to the next running auction for the respective auction pair and are thus *redistributed to all users of the DutchX protocol*! It incentivises volume and use of the protocol.  

Your individual liqudity contribution depends on your amount of Magnolia token held as a percentage of the entire Magnolia market (it is a step function):  
=>10% of Magnolia held --> 0.1% liquidity contribution  
1%-10% of Magnolia held --> 0.2% of liquidity contribution  
0.1%-1% of Magnolia held --> 0.3% of liquidity contribution   
0.01%-0.1% of Magnolia held --> 0.4% of liquidity contribution  
anything below 0.01% of Magnolia held --> 0.5% of liquidity contribution.  
  
 **The liquidity contribution could also be positive** for a trader that has lower contribution than other traders in the same pair! 

## Magnolia 
Magnolia (MGN) tokens are intrinsic to the DutchX and lower the default liquidity contribution on the DutchX Protocol.  
MGN are automatically generated and credited to users: 1 MGN is credited for trading 1 ETH worth of any whitelisted token pair (and of course trading any fraction of ETH generates the same fraction of MGN).
MGN are locked by default into a smart contract for which the user’s address is associated with a particular balance.  
A user may unlock all Magnolia associated with an address at once and after 24 hours have passed, these tokens may be transferred to another address. The new holder must then lock their tokens again (or a subset thereof) in order to use the Magnolia balance for liquidity contribution reduction.  
Magnolia are inflationary, which should incentivise an early adoption and continuous use of the DutchX protocol.  
Magnolia are not needed to participate as a seller or bidder on the DutchX.

## Whitelist
Whitelisted tokens are those that have the potential to generate Magnolia when traded in a whitelisted pair. The idea of whitelisted tokens is that no token can be added to the DutchX Protocol with the mere intention to create Magnolia and benefit from liquidity contributions.
Whitelisting will - in future - be decided by the DAO.  
This is the complete list of the [currently whitelisted tokens](https://github.com/gnosis/dx-contracts/blob/release/2.0/test/resources/approve-tokens/dxDAO_approved_tokens.js) (as per February 2019).  
They were selected based on a legal assessment of token characteristics, which suggest that legislation of major jurisdictions regulating securities, financial instruments or similar and/or mandating customer due diligence procedures do not apply to them at this point in time for the purposes of the DutchX protocol.
Regardless of being whitelisted, tokens will still first need to be added to the protocol before trading is possible.  
 
Note that whitelisted tokens are not the same as **listed** and **traded** tokens. A whitelisted token has the potential to create Magnolia tokens (used for reduction of liquidity contribution) if traded in a whitelisted pair. Tokens can be listed for trading on the DutchX protocol, albeit not whitelisted (and hence trades do not generate Magnolia); on the flip side, tokens could be whitelisted, however not listed/traded on the DutchX protocol.

## GNO
There is no special use case for GNO. It is treated as any other ERC20 token.

## OWL
In version DutchX 2.0, OWL is part of the DutchX Protocol:

### What is OWL?
- OWL is an ERC20 token. Check it out on [Etherscan](https://etherscan.io/token/0x1a5f9352af8af974bfc03399e3767df6370d82e4).
- It is a token that given GNO its utility and is creating by GNO holders locking down GNO (for a period of time).
- There has been one initial instance of creating OWL, with more to follow. Read this [communication](https://blog.gnosis.pm/generate-your-first-owl-using-gno-2205eb098f8) about it.
- At the moment, there is no generation ongoing. Further OWL generation will be publically announced.

### What is OWL used for on the DutchX?
- Useres *may* use OWL to settle half of their liquidity contribution. The rest is settled in the token they are taking part in.
- This does not affect liquidity contribution reduction. The reduction happens first, *then* half may be settled in OWL
- 1 OWL is treated as an equivalent of 1USD worth of fees.
- The OWL used will not go to any party but will instead be burnt (consumed)

### How do I use it on the DutchX?
- OWL is completely optional to use. You must set an allowance for the smart contract.
- OWL are, however, not needed to participate as a seller or bidder on the DutchX; their use is completely voluntary.

### Why would I want to use OWL?
- You might have OWL anyways as you used your GNO to generate it.
- You might be able to acquire it for less than 1USD worth and would hence reduce your liquidity contribution!

### How do I get OWL?
- See above, there was an initial generation. 
- Stay tuned for further generations. For this, you would need GNO.
- OWL may be traded on secondary markets or OTC.

## Auctioneer Powers
