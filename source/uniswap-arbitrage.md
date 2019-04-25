# DX-Uniswap-Arbitrage

## Overview
- Introduction
- Contracts
- Bots

## Introduction
Blockchains have brought with them the paradigm of programmable money. Whereas before, money could be _represented_ in software it is now a native type and a first class citizen. As such there are interesting opportunities to wield them. One such opportunity is an arbitrage between two decentralized exchanges—in our situation we are using the __DutchX__ and __Uniswap__.

Previously, making a purchase of an asset on one exchange in order to sell it at a higher price on another  entailed the risk of price movement during the operation. That movement might invalidate the original opportunity so that the arbitrageur either took a loss of profit or was left holding an asset they no longer wanted. This could occur because that process is actually asynchronous—the buyer has at least two discreet actions (the buy and the sell) and time will pass between them. In our decentralized exchange scenario we are able to combine all of our actions into one so there is no time that passes between the buy and the sell and we can eliminate the risk of price change.

This document and the software it describes can be used to execute arbitrage opportunities between __ERC-20__ tokens that are listed on both the __DutchX__ and __Uniswap__. It requires available __Ether__ to execute these orders and comes with configurable Bots that can be used to automatically execute the opportunity.

## Contracts
The DutchX uses a [proxy contract](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchangeProxy.sol) to interact with a main [DutchExchange.sol](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchange.sol) contract where there are a series of auctions constantly underway. Typically the auctions begin when there is enough sell volume to instigate them. The price of these sell auctions begin at 2x the price of the previous closing. This price decreases over time with the goal of reaching the previous closing price after 6 hours and reaching 0 after 24 hours. During this time buy orders can be made at the current price. Since the price will keep decaying until all assets have been sold, the buyer knows that they will receive at least as much as they paid for in that moment. Since they know they have purchased at least as much as the current price dictates, they are able to instantly withdraw that amount (although it is likely they will actually have purchased more than that amount in total at a lower price). The ability to withdraw at least that amount is what makes the synchronous arbitrage possible.

Uniswap has one main [Factory contract](https://github.com/Uniswap/contracts-vyper/blob/master/contracts/uniswap_factory.vy) which keeps track of all Uniswap Exchanges and is used to make new ones as well. Each Uniswap Exchange is a copy of the [Exchange template](https://github.com/Uniswap/contracts-vyper/blob/master/contracts/uniswap_exchange.vy) and contains a single pair of ERC-20 tokens or a pair between an ERC-20 and Ether (most are of the latter type). Similar to the DutchX, these contracts contain the ability to buy or sell an asset in a single transaction making our atomic swap of assets between the exchanges possible.

Our [Arbitrage Contract](https://github.com/gnosis/dx-uniswap-arbitrage/blob/master/contracts/Arbitrage.sol) needs to reference the DutchX proxy address as well as the Uniswap Factory Address. To save gas these are hard-coded for [Rinkeby](https://github.com/gnosis/dx-uniswap-arbitrage/blob/master/contracts/ArbitrageRinkeby.sol) and [Mainnet](https://github.com/gnosis/dx-uniswap-arbitrage/blob/master/contracts/ArbitrageMainnet.sol), but left as constructor arguments for [local development](https://github.com/gnosis/dx-uniswap-arbitrage/blob/master/contracts/ArbitrageLocal.sol). The main arbitrage contract comes with some abilities to manage balances on the DutchX as well as the ability to execute arbitrage opportunities.

If a specific token is cheaper on the DutchX with relation to Ether it would initially be bought from the DutchX and sold for Ether on Uniswap; This is called a `dutchOpportunity`. If a specific token is cheaper on Uniswap it would be purchased with Ether and sold on the DutchX for Ether; this is called a `uniswapOpportunity`. Each method will execute the subsequent buys and sells on the respective exchanges in a single transaction. At the end of the transaction the total amount of profit gained is confirmed. If the methods were executed when there was in fact no opportunity for an arbitrage, this will be detected and the transaction is reverted. The only potential loss is in the gas used to check the opportunity. That is why the bots used to determine when to execute are important in saving the loss of unnecessary gas expenditures.

The arbitrage contract has the following Interface:

```solidity
contract Arbitrage is Ownable {    

    /// @dev Payable fallback function has nothing inside so it won't run out of gas with gas limited transfers
    function() external payable {}

    /// @dev Only owner can deposit contract Ether into the DutchX as WETH
    function depositEther() public payable onlyOwner;

    /// @dev Only owner can withdraw WETH from DutchX, convert to Ether and transfer to owner
    /// @param amount The amount of Ether to withdraw
    function withdrawEtherThenTransfer(uint amount) external onlyOwner;

    /// @dev Only owner can transfer any Ether currently in the contract to the owner address.
    /// @param amount The amount of Ether to withdraw
    function transferEther(uint amount) external onlyOwner;

    /// @dev Only owner function to withdraw WETH from the DutchX, convert it to Ether and keep it in contract
    /// @param amount The amount of WETH to withdraw and convert.
    function withdrawEther(uint amount) external onlyOwner;

    /// @dev Internal function to withdraw WETH from the DutchX, convert it to Ether and keep it in contract
    /// @param amount The amount of WETH to withdraw and convert.
    function _withdrawEther(uint amount) internal;

    /// @dev Only owner can withdraw a token from the DutchX
    /// @param token The token address that is being withdrawn.
    /// @param amount The amount of token to withdraw. Can be larger than available balance and maximum will be withdrawn.
    /// @return Returns the amount actually withdrawn from the DutchX
    function withdrawToken(address token, uint amount) external onlyOwner returns (uint);

    /// @dev Only owner can transfer tokens to the owner that belong to this contract
    /// @param token The token address that is being transferred.
    /// @param amount The amount of token to transfer.
    function transferToken(address token, uint amount) external onlyOwner;

    /// @dev Only owner can approve tokens to be used by the DutchX
    /// @param token The token address to be approved for use
    /// @param allowance The amount of tokens that should be approved
    function approveToken(address token, uint allowance) external onlyOwner;

    /// @dev Only owner can deposit token to the DutchX
    /// @param token The token address that is being deposited.
    /// @param amount The amount of token to deposit.
    function depositToken(address token, uint amount) external onlyOwner;

    /// @dev Internal function to deposit token to the DutchX
    /// @param token The token address that is being deposited.
    /// @param amount The amount of token to deposit.
    function _depositToken(address token, uint amount) internal;

    /// @dev Executes a trade opportunity on DutchX. Assumes that there is a balance of WETH already on the DutchX
    /// @param arbToken Address of the token that should be arbitraged.
    /// @param amount Amount of Ether to use in arbitrage.
    /// @return Returns if transaction can be executed.
    function dutchOpportunity(address arbToken, uint256 amount) external onlyOwner;

    /// @dev Executes a trade opportunity on uniswap.
    /// @param arbToken Address of the token that should be arbitraged.
    /// @param amount Amount of Ether to use in arbitrage.
    /// @return Returns if transaction can be executed.
    function uniswapOpportunity(address arbToken, uint256 amount) external onlyOwner;

}
```

## Bots
Gnosis has developed a sophisticated system of Bots available in the [dx-services](<https://github.com/gnosis/dx-services>) repository on Github. These services are primarily used to populate auctions with assets and execute buy orders if a price reaches a threshold below what a seller was willing to sell at. This repo now includes services to facilitate arbitrage opportunities as well. These can be executed manually via the Command Line Interface (CLI) or via auto-executed Bots.

In order to calculate whether there currently exists an arbitrage opportunity the bots periodically check the current price of an asset on both Uniswap and the DutchX. It is possible that the current price on Uniswap will be lower than the DutchX while there may still not be an arbitrage opportunity. This is because Uniswap has a great deal of price slippage that depends on how liquid the actual market is. After an initial arbitrage opportunity is detected it is checked incrementally how large of a purchase order would be possible on Uniswap before the price slippage would ruin the opportunity. After that limit is reached, the potential profit gained is checked against the gas cost of executing the order. If there is still a potential profit, the order is executed.

With regard to the arbitrage CLI the following commands are available:

```bash
deposit-ether <amount> [--arbitrage-contract address]
  Deposit any Ether in the contract to the DutchX as WETH

deposit-token <amount> <token> [--arbitrage-contract address]
  Deposit any token in the contract to the DutchX

dutch-opportunity <token> <amount> [--arbitrage-contract address]
  Execute a Dutch Opportunity transaction with Arbitrage contract

get-balance [token] [--arbitrage-contract address]
  Get the arbitrage contract balance of any token (blank token for Ether)

manual-trigger <token> [--arbitrage-contract address] [--minimum-usd-profit profit]
  Attempt an arbitrage

transfer-ether <amount> [--arbitrage-contract address]
  Transfer Arbitrage contract ETH to contract owner (amount = 0 transfers total balance)

transfer-ownership <arbitrage-address> <new-owner-address>
  Transfer ownership of the Arbitrage contract

transfer-token <amount> <token> [--arbitrage-contract address]
  Transfer Arbitrage contract token balance to contract owner

uniswap-opportunity <token> <amount> [--arbitrage-contract address]
  Execute an Uniswap Opportunity transaction with Arbitrage contract

withdraw-ether <amount> [--arbitrage-contract address]
  Withdraw WETH from DutchX and convert to Ether

withdraw-token <amount> <token> [--arbitrage-contract address]
  Withdraw token from DutchX

withdraw-transfer-ether <amount> [--arbitrage-contract address]
  Withdraw WETH from DutchX, convert to Ether and transfer to owner address
```

With regard to the bots the following config could be used for checking arbitrage between Ether and Raiden as well as Ether and Omisego:

```
{
  name: 'Arbitrage bot',
  factory: 'src/bots/ArbitrageBot',
  botAddress: '0x123',
  markets: [
    { tokenA: 'WETH', tokenB: 'RDN' },
    { tokenA: 'WETH', tokenB: 'OMG' }
  ],
  arbitrageContractAddress: '0x234',
  minimumProfitInUsd: 5, // $5
  notifications: [{
    type: 'slack',
    channel: 'CABG321'
  }],
  checkTimeInMilliseconds: 60 * 1000 // 60s
}
```
