# Add a trading token pair
The DutchX is an open platform, and as such, anybody can add it's token by 
themselves.

Check out this slides to find out more about the advantages and some information
about <a href="_static/docs/DutchX_Handbook_New_Tokens.pdf" download>Listing a token in the DutchX</a>.

## Using the Smart Contracts
There are several ways you can add a token to the DutchX. All of them end up 
using the `addTokenPair` function in the 
[**DutchExchange.sol**](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchange.sol) 
contract.

To add the token pair using the Smart Contract, it's useful to read the guide 
og [Build on top of the DutchX](./build-on-top-of-dutchx.html).

To invoke the `addTokenPair` operation, we need to do it through the address 
of the deployed [**DutchExchangeProxy.sol**](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchangeProxy.sol)
  * Please, read more about the Proxy Pattern for Smart Contracts in 
  this <a href="https://blog.gnosis.pm/solidity-delegateproxy-contracts-e09957d0f201" target="_blank">Solidity DelegateProxy</a> post.

Let's assume that we want to add `RDN-WETH` token pair. 

To add a token pair you will neeed the folowing information:
* **Address of the first token**: `WETH` in this case
  * When you list a token for the first time it's mandatory to use 
    `Wrapped Ether` (`WETH`) as the other token in the pairing.
  * Check out this [Information about what is WETH](https://weth.io/) to learn more
    about Wrapped Ether.
  * The addresses for `WETH` are:
    * `mainnet`: [0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2](https://etherscan.io/token/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2) 
    * `rinkeby`: [0xc778417e063141139fce010982780140aa0cd5ab](https://rinkeby.etherscan.io/token/0xc778417e063141139fce010982780140aa0cd5ab)
* **Address of the token you want to add**: `RDN` in this case.
  * This is the address of the `ERC20` token you want to add.
  * For example, in mainnet `RDN` token has the address [0x255Aa6DF07540Cb5d3d297f0D0D4D84cb52bc8e6](https://etherscan.io/token/0x255aa6df07540cb5d3d297f0d0d4d84cb52bc8e6)
* **Price of the token pair**:
  * This is the price you claim that your token against the `WETH`.
  * Note that you there's no benefit on adding a very low or very high price,
    quite the opposite.
  * If you decide to use a very low price, anyone could participate in the 
    auction and buy cheap the `WETH` you deposit when you add a token pair.
  * If you set it to high, the auction will take more time to reach the market 
    price. It'll end up closing with the market price.      
* **Funding for first token** (in Weis): For example `20 WETH` (More than `10.000$` when this guide was written)
  * This is the amount you are going to deposit for the first auction of the token pair.
  * It's important to know that,in order to add a token, you should surplus the
    **minimun threshold for adding a token pair** (`10.000$` of the token). For 
    the calculation of the worth in USD of your tokens, the DutchX will use two
    things:
      * **The price you provide**: This is the price you claim your token is 
        worth.
      * **The price of the `WETH-USD`**: The DutchX uses a oracle that will tell
      you
  * Your account should have this amount of token in it's DutchX balance. So, it's 
  important to know that before invoking this you should have done two prior 
  operations:
    * **Approve the DX to withdraw tokens in your name** 
    [ERC20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md) 
    `approve` of at least this amount in favour of the 
    [DutchExchangeProxy address](/smart-contracts_addresses.html) so the DutchX is entitled to
    deposit the amount into yout balance when you invoke a `deposit`.
    * **Deposit funds in your DutchX balance**: 
    [**DutchExchange.sol**](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchange.sol) 
    `deposit` of at least this amount.  
* **Funding for the second token**:
  * This is not mandatory, so you can set a `0` here.
  * It's enough to provide liquidity in any of the sides. If one of the tokens 
    is `WETH` (this case), you must provide it in that token.

Once you have all the information and you have deposited in the DutchX the amount
of the funding, you are ready to invoke the `addTokenPairFunction`, in this case
would be something like: 

```js
// Get the Dutch Exchange instance using the DuthExchange contract and the 
// DuthExchangeProxy addres.
const dx = DuthExchange.at(DuthExchangeProxy.address)

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
  // 20 WETH
  20000000000000000000,
  // 0 RDN
  0,
  // Check price of RDN-WETH in:
  //  https://www.coingecko.com/en/price_charts/raiden-network/eth
  //  1 ETH = 584 RDN
  584, // numerator
  1    // denominaor
)
```

## Use the add-token-pair script
To make things easier, there's a [truffle script](https://github.com/gnosis/dx-contracts/blob/master/src/truffle/add-token-pairs.js) in the 
[dx-contracts](https://github.com/gnosis/dx-contracts) project.

So the steps would be:

**1. Clone the the repo and install the dependencies**:
```bash
git clone https://github.com/gnosis/dx-contracts.git
cd dx-contracts
npm install
```

**2. Create a file with the information required for the operation**
  * Read the required information in the previous 
  * You can use [01_RDN-WETH.js](https://github.com/gnosis/dx-contracts/blob/master/test/resources/add-token-pair/mainnet/01_RDN-WETH.js)
    and [WETH_RDN.js](https://github.com/gnosis/dx-contracts/blob/master/test/resources/add-token-pair/mainnet/WETH_RDN.js) 
    as an example on how to provide the information.
  * Save your config file in the current directory, for example `ABC-WETH.js`

**3. Run first in dry-run mode**: It'll validate if everything is ok for adding 
the token pair, but it won't execute it:
  * Use the mnemnonic of the account that have deposited the initial funding.
  * Use the file you created in the previous step (i.e. `./ABC-WETH.js`)
  * Provide the name of the network wete you want to add the token pair `mainnet` or `rinkeby`.
  * Don't forget the `--dry-run`
```bash
MNEMONIC="your secret mnemonic ..." npm run -- add-token-pairs -f ./ABC-WETH.js --network mainnet --dry-run
```

If everything went smoothly, you should now be able to execute it for real.
Otherwise, the command will tell you what is the problem and what you need to 
do in orther to solve it.

**4. Run the script withouth the dry-run**:
```bash
MNEMONIC="your secret mnemonic ..." npm run -- add-token-pairs -f ./ABC-WETH.js --network mainnet
```

