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
Magnolia (MGN) tokens lower the default liquidity contribution on the DutchX Protocol.  
MGN are automatically generated and credited to users: 1 MGN is credited for trading 1 ETH worth of any whitelisted token pair (and of course trading any fraction of ETH generates the same fraction of MGN).
MGN are locked by default into a smart contract for which the user’s address is associated with a particular balance.  
A user may unlock all Magnolia associated with an address at once and after 24 hours have passed, these tokens may be transferred to another address. The new holder must then lock their tokens again (or a subset thereof) in order to use the Magnolia balance for liquidity contribution reduction. 

## Whitelist
Whitelisted tokens are those that have the potential to generate Magnolia when traded in a whitelisted pair. The idea of whitelisted tokens is that no token can be added to the DutchX Protocol with the mere intention to create Magnolia and benefit from liquidity contributions.
Whitelisting will - in future - be decided by the DAO.  
This is the complete list of the [currently whitelisted tokens](https://github.com/gnosis/dx-contracts/blob/release/2.0/test/resources/approve-tokens/dxDAO_approved_tokens.js) (as per February 2019).  
They were selected based on a legal assessment of token characteristics, which suggest that legislation of major jurisdictions regulating securities, financial instruments or similar and/or mandating customer due diligence procedures do not apply to them at this point in time for the purposes of the DutchX protocol.
Regardless of being whitelisted, tokens will still first need to be added to the protocol before trading is possible. 
