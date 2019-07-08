# Listing a token
Some information that you might find relevant when thinking about adding a token to the DutchX protocol:
- It is completely permissionless and decentralized: anyone can add a token pair based on the same rules of the smart contract
- No central entity decides on which tokens become tradable!
- It is completely free (gas costs, of course, incur)
- If a token  is available to trade on the DutchX it does not necessairly imply that there is enough liquidity to actually be traded
- A token that is available to trade is not the same as a [*whitelisted*](https://dutchx.readthedocs.io/en/latest/basic-mechanism.html#whitelist) token
- **Gnosis Ltd does not decide on which tokens become tradable on the DutchX open protocol!**

## The theory to list
- A new token always has to be added as a pair with WETH
  - For this, the first auction that is initiated has to be funded with an equivalent of 1k USD worth of WETH
  - The initiator has to set a price for WETH-NewToken; the auction will start at twice this price
    - There is an incentive to set the correct price: if it is too low, the initiator sells their WETH below marketprice. if it is too high, the auction will run longer.
   - The auction starts after 6 hours 
   - No need to add two sides
   - Someone should be ready to bid 
   - Adding is free: the funding is not "invested" or "lost", it is merely exchanged
   - After this, auction can run as defined in the smartc contracts:
      - Opposite auctions start and run at the same time (i.e. A-WETH (sellToken is A, buyToken is WETH) & WETH-A (sellToken is WETH, buyToken is A))
     - There is always only one auction running at the same time for a particular pair
     - Subsequent auctions only start if the sellVolume of both opposite auctions is each above USD 1k
   
## Some benefits of being traded on the DutchX
- Reduces reliance on centralized exchanges; the DutchX is non-custodial in nature
- Open: Incentivises building on top of a permissionless protocol, low barriers to entry and set and unbiased rules to be enforced by the [dxDAO](https://dutchx.readthedocs.io/en/latest/dxDAO.html)
- A fair price finding mechanism and a redistribution of paid fees to the users of the DutchX
- Fully on-chain: smart contracts can interact directly because there is no need for off-chain receipt/signing of a transaction
- The first fully decentralized & upgradable token trading protocol
- Particularly great for low-liquidity tokens due to the duration of the batching of the sell Volume and the single clearing price
- Don't forget that the liquidity contribution retained in the ecosystem remain allocated to the same token pair. These contributions are added to the sell side of the next auction without any dilution with other pairs on the DutchX
- Provides an reliable on-chain [price oracle](https://dutchx.readthedocs.io/en/latest/price-oracle.html)
- There are [several interfaces](https://dutchx.readthedocs.io/en/latest/interfaces.html) available for technical and non-technical traders

## Liquidity
**Please be aware: Having listed, does not mean that the token is traded. For this - of course - sufficient liquidity is needed.** 
- It is recommended that the lister initially also ensures that there is enough liquidity for the listed token pair
- It is a two-sided market place and for the network effects to work, the market has to function first
- There are two relatively easy options available right now:
  - [Check out the section on running minimal liquidity bots](https://dutchx.readthedocs.io/en/latest/bots-market-making.html)
  - [Check out the section about market makers](https://dutchx.readthedocs.io/en/latest/market-makers.html)

## Availabilty of different pairs
- Each token has to first be added as a pair with WETH
- Two tokens that are already available with WETH on the DutchX, may be initiated with one another
- For this, no price setting is needed (as both are available with WETH)
- For the listing of a pair that is not WETH, the accumulated sell Volume amount of both opposite auctions has to be at least 1K USD.

## Technical steps
- Read the code [here](https://github.com/gnosis/dx-contracts/blob/1fc99740a86a1635c9bf856a370b16295915b76d/contracts/DutchExchange.sol#L347)
- Check the [Developer Guide](https://dutchx.readthedocs.io/en/latest/add-token-pair.html)
