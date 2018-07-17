# Public API
The API is an alternative and easier access to the information on
the smart contracts.

It was built to make the information more accessible, so it hides the barriers 
that a newcomer may find in the Ethereum development.

The API is accesible for:
  * **Mainnet**: [https://dutchx.d.exchange/api](https://dutchx.d.exchange/api)
  * **Rinkeby**: [https://dutchx-rinkeby.d.exchange/api](https://dutchx-rinkeby.d.exchange/api)

The API is Open Source, so anyone can run it in it's own server.

It provides read-only access. For any operation that needs to write in the 
blockchain, you'll need to do it using your own node (or infura). Checkout 
how to do this by reading [Build on top of the Dutch Exchange](./build-on-top-of-dutchx.html)

The API logic is implemented in the [DutchX Services](https://github.com/gnosis/dx-services),
for more information checkout [DutchX as an open platform](./dutchx-as-an-open-platform.html)