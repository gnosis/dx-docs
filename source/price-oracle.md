# Price Oracle
The DutchX smart contract has one on-chain price oracle function, which is always the *weighted average price of the last ended auction of the Token with respect to ETH*. Weighted average by volume of the two opposite auctions (Token-ETH and ETH-Token). It can be used by other smart contracts. Obviously it’s not updated as often as in other exchanges but is hence also much less volatile. Check out the function in the [code](https://github.com/gnosis/dx-contracts/blob/1fc99740a86a1635c9bf856a370b16295915b76d/contracts/DutchExchange.sol#L936).   

For various applications, this price feed might not be sufficient. More so, as it only consists of data of *one* auction pair, it might not only be gamable, its accuracy might also depend on the volume of that particular auction pair.  

Taking a median may remedy these problems. Note that the median of a number of auctions on the DutchX is taken over time (rather than across many platforms at the same time), which may make it not as usable for some finance related decentralized applications, which need accurate prices by the second.  

The price oracle smart contract, however, might be very useful for other applications, such as the calculation of the token value used on the vote staking interface of the dxDAO.  

**How does this DutchXPriceOracle work?**  

It takes the median of the last 9 auctions of that token pair on the DutchX, if they have run consecutively (i.e. constant liquidity is important), else it will not return a price feed.  
- This price feed also only works for tokens with (W)ETH  
- There are two functions: getPrice and getPriceCustom
    - getPrice only works for actually [whitelisted tokens](https://dutchx.readthedocs.io/en/latest/mechanism.html#whitelist)
    - getPriceCutstom allows customization (for other tokens).  
    
Check out this [Price Oracle API endpoint](https://dutchx.d.exchange/api/docs/#!/Prices/getOraclePrice).

Check out the [code](https://github.com/gnosis/dx-price-oracle/tree/master).
