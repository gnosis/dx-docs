# Deposit tokens
The DutchX allows to echange ERC20 compatible tokens.

In order to post sell orders, buy orders or add token pairs, you first need to 
deposit the tokens in the DutchX, so it's important you understand how to:
* Wrap ether
* Set an allowance for the DutchX
* Deposit in the DutchX

## WETH
Ether is not an ERC20 token, this is why we need to wrap it first.

Technically, this means that we need to **send some ether to the `deposit` function in a token contract called WETH (Wrapped Ether))**:
* WETH contract: https://rinkeby.etherscan.io/address/0xc778417e063141139fce010982780140aa0cd5ab#code
* Info about WETH: https://weth.io
* More info about WETH: https://blog.0xproject.com/canonical-weth-a9aa7d0279dd

## Allowance (any ERC20 token)
Other important thing we should know, is that the `deposit` function in DutchX, 
will call the ERC20 token contract `transferFrom` function to withdraw the 
amount for the user:
* This `transferFrom` will fail if the user don't set an allowance of at least
  the deposited amount for the DutchX proxy address (entry point for DutchX)
* So you first need to invoke the `approve` function
* This step is **mandatory** for WETH and for any other ERC20 token.

## Deposit
The DutchX deposit operation will allow you to add tokens to your balance.

When you have balance in the DutchX you'll be able to:
* Submit sell orders
* Submit buy orders
* Add token pairs

## Sequence diagram
This sequence diagram will show you the 3 important operations we will do in 
this example:
1. **Wrap 0.1 WETH**: Remember Ether is not ERC20 compatible, so we need to do this 
  step (`deposit` function on WETH contract).
2. **Set allowance, so DutchX proxy can transfer 0.1 WETH**: Otherwise the
  deposit will fail, because the DutchX wouln't be entitled to do the operation.
3. **Deposit 0.1 ETH in DutchX proxy**: If we did the two prior steps, the user
  will have 0.1 WETH more in it's balance.

![Sequence for deposit](./docs/sequence-deposit.png "Sequence for deposit")

## How to do it?
In [this guided example](https://github.com/gnosis/dx-examples-dev/tree/master/01_basic-web-deposit) you 
will make a dApp that wraps ether, sets the allowance and deposit into the dutchx.

Also you can use the [CLI](./cli.md)
