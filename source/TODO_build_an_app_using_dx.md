# Get started - Use DX in your project
Add it to your project:

```bash
# Install the dependencies
yarn add truffle-contract @gnosis.pm/dx-contracts --save # or npm install @gnosis.pm/dx-contracts --save
```

You will find the compiled truffle contracts in the `build/contracts` folder,
these contract abstractions will also contain the addresses for the DX for 
**mainnet** and the **testnets**.

For example:
```js
const contract = require('truffle-contract')

// Create the truffle contracts
const DutchExchangeProxy = contract(require('@gnosis.pm/dx-contracts/build/contracts/DutchExchangeProxy'))
const DutchExchange = contract(require('@gnosis.pm/dx-contracts/build/contracts/DutchExchange'))

// Setup your provider
// provider = ...
DutchExchange.setProvider(provider)
DutchExchangeProxy.setProvider(provider)

// Get the contract instance
DutchExchangeProxy.deployed(async proxy => {
  const dx = DutchExchange.at(proxy.address)

  // Use any of the dx methods
  const token1 = '0x123456'
  const token1 = '0x654321'
  const auctionIndex = await dx.getAuctionIndex.call(token1, token2)
  console.log(auctionIndex)
})
```
