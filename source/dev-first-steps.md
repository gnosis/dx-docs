# Develop on top of DutchX
For folowing this, you should be familiar with:
* Basics about Ethereum network
* Truffle projects
* Node and NPM

## Create your new cool-app
The easiest way to get started is to create a new node project that depends on
the [dx-contracts](https://github.com/gnosis/dx-contracts/tree/master/contracts) 
project.

**DutchX** publish a NPM package with:
* All the compiled contracts (ABI, meta info, addresses)
* Migration code (useful for `development`)
* Some scripts

So Just follow the steps and create your `cool-app` out of this example:
[https://github.com/gnosis/dx-example-build-on-top-of-dutchx/tree/master/example_01_build-of-top-of-dx](https://github.com/gnosis/dx-example-build-on-top-of-dutchx/tree/master/example_01_build-of-top-of-dx)

## Create your own migrations - Add your own token pair
After you have your `cool-app` as a truffle project that in it's first migration
do the DutchX deployment, we are ready to create our own migrations.

You can add your own migrations for deploying your own contracts, or to invoke 
any setup on the DutchX.

To show how simple it is to setup things, we will add our own token pair in the 
DutchX.

Just add the folowing migration:
```js

```


## Use the DutchX in your app
TODO: use truffle contract, invoke add token pair, participate auction

## Use DutchX as a Price Oracle
TODO: 

## Test Rinkeby
TODO:

## Go live - Mainnet
TODO: