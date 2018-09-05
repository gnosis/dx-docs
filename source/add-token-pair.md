# Add a token pair
The DutchX is an open platform, and as such, anybody can add a token pair to trade. 

Check out these slides to find out more
about <a href="_static/docs/DutchX_Handbook_New_Tokens.pdf" download>**listing a token on the DutchX**</a>.

There are several ways to add a token pair to the DutchX. All of them end up
using the `addTokenPair` function in the
[**DutchExchange.sol**](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchange.sol)
contract.

To invoke the `addTokenPair` operation, we need to do it through the address
of the deployed [**DutchExchangeProxy.sol**](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchangeProxy.sol)
  * Please, read more about the Proxy Pattern for Smart Contracts in
  this <a href="https://blog.gnosis.pm/solidity-delegateproxy-contracts-e09957d0f201" target="_blank">Solidity DelegateProxy</a> post.

## 1. Get the information for adding a token pair
Let's assume we want to add the `RDN-WETH` token pair.

To add a token pair you will need the following information:
* **Address of the first token**: `WETH` in this case
  * When you list a token for the first time it's mandatory to use
    `Wrapped Ether` (`WETH`) as the other token in the pairing.
  * Check out this [this link](https://weth.io/) in order to learn more
    about Wrapped Ether.
  * The addresses for `WETH` are:
    * `mainnet`: [0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2](https://etherscan.io/token/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)
    * `rinkeby`: [0xc778417e063141139fce010982780140aa0cd5ab](https://rinkeby.etherscan.io/token/0xc778417e063141139fce010982780140aa0cd5ab)
* **Address of the token you want to add**: `RDN` in this case.
  * This is the address of the `ERC20` token you want to add.
  * For example, on the mainnet `RDN` token has the address [0x255Aa6DF07540Cb5d3d297f0D0D4D84cb52bc8e6](https://etherscan.io/token/0x255aa6df07540cb5d3d297f0d0d4d84cb52bc8e6)
* **Price of the token pair**:
  * This is the price you claim that your token has against the other token, 
    that's `WETH-RDN` price in this case (`584 RDN/ETH` by the time this 
    document was written)
  * Note that there's no benefit on adding the wrong price:
    * If you decide to use a very low price, anyone could participate in the
      auction and buy cheap the `WETH` you deposit when you add a token pair.
    * If you set it to high, the auction will take more time to reach the market
      price. It'll end up closing with the market price.
    * If you are confused about how the mechanism work, read the 
      [Blog posts](https://blog.gnosis.pm/tagged/dutchx), and for a very detailed 
      mathematical explanation, check out the 
      [Smart Contract Documentation](smart-contract-documentation.html).
* **Funding for first token** (in Weis): For example `18 WETH` (more than 
    `10.000$`, note we use `584 RDN/ETH` as the price)
  * This is the amount you are going to deposit for the first auction of the token pair.
  * It's important to know that, in order to add a token, you should surplus the
    **minimum threshold for adding a token pair** (`10.000$` of the token). For
    the calculation of the worth in USD of your tokens, the DutchX will use two
    things:
      * **The price you provide**: This is the price you claim your token is
        worth.
      * **The price of `WETH-USD`**: The DutchX uses an oracle that reports
        the current price for this pairing.
  * Your account should have this amount of tokens in its DutchX balance. Don't
    worry about this right now, because it's covered in the **Fund the account**
    section.
* **Funding for the second token**:
  * This is not mandatory, so you can set a `0` here.
  * It's enough to provide liquidity in any of the sides. If one of the tokens
    is `WETH` (this case), you must provide it in that token.

## 2. Fund the account
Once you know the amount you need to do the deposit of the token (`18 WETH` in the 
example).

In order two add balance to your account, we need to invoke two operations in the
smart contracts:
  * **Approve the DX to withdraw tokens in your name**: This is a call to the 
  [ERC20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md)
  `approve` for the funding token (`WETH` in this case). You must approve at 
  least the funding amount, and use the 
  [DutchExchangeProxy address](./smart-contracts_addresses.html) contract, so 
  the DutchX is entitled to deposit the amount into your balance when you 
  invoke the next operation (`deposit`).
  * **Deposit funds in your DutchX balance**: This is a call to 
  [**DutchExchange.sol**](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchange.sol)
  `deposit`. You must use at least the funding amount.

The easiest way to invoke these two operations is to use the `CLI`, so please 
set it up by following the steps described in the [CLI](./cli.html) page.


**1. Verify that your account has the tokens**
We are trying to deposit some tokens into the DutchX, so first we should make 
sure they are in our balance:

```bash
./cli balances --account <your account address here>
```

**2. Do the deposit**
Once the `CLI` is ready, just execute the deposit operation, make sure:
* You use the right **network** (`rinkeby` or `mainnet`)
* You use the right **mnemonic** (the one that has the tokens you want 
to deposit into the DutchX)
* **NOTE**: the `CLI` will automatically do a `approve` and a `deposit`. Aditionally,
  in the case of `WETH`, it'll wrap `Ether` if you don't have enough balance.

```bash
# Wrap, approve and deposit into the DutchX
./cli deposit 18 WETH
```

**3. Verify your new balance on the DutchX**
```bash
./cli balances --account <your account address here>
```


## 3. Add the token pair
Once you have all the information and you have deposited in the DutchX the funding amount, you are ready to invoke the `addTokenPairFunction`.

There are several ways to do this:
* **Use the `add-token-pair` script**: This is the recommended one, since it 
  also performs some validations and shows help messages.
* **Use truffle consolle**: Since the 
  [DutchX Smart Contracts](https://github.com/gnosis/dx-contracts) is a truffle
  project, you can use the console to add the token pair or invoke any other 
  logic of the contract.
* **From a migration in your project**: Use this option if you are building a 
  project and you want to also add the tokens in your local development node.
* **Using the CLI**: The `CLI` has also a `add-token-pair` that uses the same 
  format as the `add-token-pair` script.

### 3a. Use the add-token-pair script (`recommended`)
To make things easier, there's a [truffle script](https://github.com/gnosis/dx-contracts/blob/master/src/truffle/add-token-pairs.js) in the
[dx-contracts](https://github.com/gnosis/dx-contracts) project.

So the steps would be:

**1. Clone the the repo and install the dependencies**:

```bash
# Clone the repo and cd into the project
git clone https://github.com/gnosis/dx-contracts.git
cd dx-contracts

# Install the dependencies
npm install

# Compile contracts and inject the network info
npm run restore
```

**2. Create a file with the information required for the operation**
  * Read the required information in the previous section
  * You can use [01_RDN-WETH.js](https://github.com/gnosis/dx-contracts/blob/master/test/resources/add-token-pair/mainnet/01_RDN-WETH.js)
    and [WETH_RDN.js](https://github.com/gnosis/dx-contracts/blob/master/test/resources/add-token-pair/mainnet/WETH_RDN.js)
    as an example on how to provide the information.
  * Save your config file in the current directory, for example `ABC-WETH.js`

**3. Run it first in dry-run mode**: 

It'll check if everything is ok for adding the token pair, but it won't execute 
the transaction:
  * Use the mnemnonic of the account that deposited the initial funding.
  * Use the file you created in the previous step (i.e. `./ABC-WETH.js`)
  * Provide the name of the network in which you want to add the token pair: `mainnet` or `rinkeby`.
  * Don't forget the `--dry-run`

```bash
MNEMONIC="your secret mnemonic ..." npm run -- add-token-pairs -f ./ABC-WETH.js --network mainnet --dry-run
```

If everything went smoothly, you should now be able to execute it for real.
Otherwise, the command will tell you what is the problem and what you need to
do in order to solve it.

**4. Run the script withouth the dry-run**:
```bash
MNEMONIC="your secret mnemonic ..." npm run -- add-token-pairs -f ./ABC-WETH.js --network mainnet
```

### 3b. Using truffle console
Since the [DutchX Smart Contracts](https://github.com/gnosis/dx-contracts) is a 
truffle project, you can use the console to add the token pair or invoke any 
other logic of the contract.

So the steps would be:

**1. Clone the the repo and install the dependencies**:

```bash
git clone https://github.com/gnosis/dx-contracts.git
cd dx-contracts
npm install
```

**2. Enter into the truffle console**

Make sure you:
  * Use the mnemnonic of the account from which the initial funding was deposited.
  * Provide the name of the network in which you want to add the token pair: `mainnet` or `rinkeby`.

```bash
MNEMONIC="your secret mnemonic ..." truffle console --network mainnet
```

**3. In the truffle console**

Enter the following commands, one by one:
```js
// Get the DutchExchange instance using the DuthExchange contract and the
// DuthExchangeProxy addres.
DutchExchangeProxy.deployed().then(p => proxy = p)
dx = DutchExchange.at(proxy.address)

// Add token pair
/*
addTokenPair(
  address token1,
  address token2,
  uint token1Funding,
  uint token2Funding,
  uint initialClosingPriceNum,
  uint initialClosingPriceDen
)
*/
dx.addTokenPair(
  // WETH
  '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',

  // RDN
  '0x255Aa6DF07540Cb5d3d297f0D0D4D84cb52bc8e6',  

  // 18 WETH
  18000000000000000000,

  // 0 RDN
  0,

  // Check price of RDN-WETH in:
  //  https://www.coingecko.com/en/price_charts/raiden-network/eth
  //  1 ETH = 584 RDN
  584, // numerator
  1    // denominaor
)
```

### 3c. From a migration in your code
To add the token pair using migrations, you should first be familiarized on 
how to build on top of the DutchX.

Make sure you have completed these two guides:
* [Build on top of the DutchX](./build-on-top-of-dutchx.html)
* [Use DutchX as an Oracle](./use-dutchx-as-an-oracle.html)

After those guides, you should be able to create a new migration like this one:

```js
/* global artifacts */
/* eslint no-undef: "error" */
const DutchExchange = artifacts.require("DutchExchange")

module.exports = function (deployer, network, accounts) {
  return deployer
    deployer
      // Make sure DutchX is deployed
      .then(() => DutchExchangeProxy.deployed())
      .then(dxProxy => {
        // Get a DutchX instance
        const dx = DutchExchange.at(dxProxy.address)

        // Add your token pair
        return dx.addTokenPair(
          // WETH
          '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',

          // RDN
          '0x255Aa6DF07540Cb5d3d297f0D0D4D84cb52bc8e6',  

          // 18 WETH
          18000000000000000000,

          // 0 RDN
          0,

          // Check price of RDN-WETH in:
          //  https://www.coingecko.com/en/price_charts/raiden-network/eth
          //  1 ETH = 584 RDN
          584, // numerator
          1    // denominaor
        )
      })
    DutchExchangeProxy
}
```

### 3d. Using the CLI
The `CLI` has also an `add-token-pair` operation that uses the same format as the 
`add-token-pair` script.

Usually, it is preferable to use the `add-token-pairs` script instead of the `CLI`,
it has some advantages, so consider using it.

To use the CLI:

**1. Create a file like the one described in add-token-pair script section**

For example `./ABC-WETH.js`

**2. Execute the add-token-pair operation**

Execute the command, and make sure:
* You use the right **network** (`rinkeby` or `mainnet`)
* You use the right **mnemonic** (the one that has the tokens in its DutchX 
  balance)

```bash
./cli add-token-pair --file ./ABC-WETH.js
```
