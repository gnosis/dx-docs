# ERC20 pooling contract for MGN

### Purpose of the contract
The MGN pooling contract works on top of the DutchX trading protocol. The purpose is for anyone to be able to participate easily in trades on the DutchX in order to generate Magnolia. 
Users may participate in this pool with their funds, which they will reiceve back at the end of the trading period (or more precisely: the value of their deposit at the end of the pooling period, which may have increased or decreased). 
The user will also receive the share of their MGN that was generated using their funds.

### Logic of the contract
- The contract is set to run a certain amount of time (one for WETH-Token and one for Token-WETH)
- The contract uses all funds to continuously take part (with all funds) in the sell side of the auction
- The contract claims back the receiving token after an auction has finished and takes part in the sell side of the opposite auction
- This process continues until the pre-defined time has been reached and an even number of auctions have  been run
- [Magnolia](https://dutchx.readthedocs.io/en/latest/mechanism.html#magnolia) is generated based on the rules of the DutchX (the pair has to be [whitelisted](https://dutchx.readthedocs.io/en/latest/mechanism.html#whitelist))

### Users' actions
As the purpose is easy participation for a user, only three actions have to be conducted:
- The user may **deposit funds** (one defined ERC20 token) at any point in time before the pooling time has ended (and may deposit more throughout time)
- The user may only **claim back** the **deposited funds** at the end of the pre-defined pooling time. *Note that the funds may have been subject to price increases or decreases*. Funds are received back in the same token the user deposited.
- The user may also **claim their** share of **Magnolia** (this is only possible at the end of the pooling period + 24hours later)
- The user does not pay gas for the trading activity

### Application to any ERC20 token
- Note that the contract is open source and may be deployed by anyone (ERC20 token to be specified upon deployment)
- Note that the deployment is always launching two contracts, one represeting ERC20 - WETH and the other representing the WETH - ERC20 trading pair, so that the both auctions can get liquidty. 
- Note that at the same time also a bot should be run that claims on behalf of the smart contract and triggers the next participation (this is the bot paying gas) 
- Note that though this ensures sell-side liquidity, it is highly advised to ensure the bidder side has also sufficient liquidity to buy up the sell-orders

### Available interface
*Information to follow*  
*Take part with GNO here (link to follow)*

### Code and audit
- MGN-Pooling smart contract [Github Repo](https://github.com/gnosis/dx-mgn-pool)
- Script of [automated participation bot](https://github.com/gnosis/dx-mgn-pool/tree/master/scripts)  
- [Interface Repo](https://github.com/gnosis/dx-mgn-pool-react)
- [Audit report](https://github.com/g0-group/Audits/blob/master/DX-MGN-POOL.md)
