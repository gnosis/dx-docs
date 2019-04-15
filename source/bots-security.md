# Security
As soon as you start using your bots with real funds. There will be security trade-offs. If you run the bots in a regular cloud server with a MNEMONIC phrase or a Private key, if an attacker breaks your server security and is able to reveal those secrets, would easily steal all your funds.

One solution we developed to mititate that risk is using multi signature software for holding the funds, specifically [Gnosis Safe Contracts](https://github.com/gnosis/safe-contracts) in conjuction with a [Safe module](https://github.com/gnosis/safe-modules/blob/master/contracts/DutchXCompleteModule.sol) that is operated through a regular account (with Mnemonic / private key) but with restricted access, the scope of actions is limited to those related with posting orders and depositing tokens, but not the possibility to withdraw funds from the DX. In case you want to withdraw the funds, you need to sign a transaction with the safe contract owners (should be different accounts than the operators).

This setup is a bit complex to setup from the scratch so for making it easier to manage, we created a [CLI](https://github.com/gnosis/dx-safe-cli)

The main roles involved are:

1. **Safe contract.** It's the contract that holds the tokens and Ether used for the DutchX. It should have at least two owners and two required confirmations.
2. **Safe module (DutchXComplete or DutchXSeller).** Has to be enabled by the safe contract, so it can execute transaction on behalf of the safe. It limits the actions to: deposit, approve tokens, wrap ETH, post sell order, post buy order (only in complete version) and claiming.
3. **Operator.** Regular account that interacts with the safe-module. This is the account the bots will use to generate the transactions. Need to have a bit of ether for paying the transaction fees. It doesn't have tokens.
4. **Whitelisted tokens.** Tokens allowed to be used in the DX by Safe module.