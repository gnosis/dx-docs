# API
The API is an alternative and easier way to access the information on
the smart contracts.

It was built to make the information more accessible, so it hides the barriers
that a newcomer to Ethereum development may find.

The API is accessible for:
  * **Mainnet**: [https://dutchx.d.exchange/api](https://dutchx.d.exchange/api)
  * **Rinkeby**: [https://dutchx-rinkeby.d.exchange/api](https://dutchx-rinkeby.d.exchange/api)

The API provides a simple way to browse over all methods:

![API docs](_static/api-docs.png)

You can also use the **TRY** button to test the endpoint:

<p align="center">
  <img src="_static/api-docs-try-functionality.png" width="500px" alt="Try endpoint" />
</p>

The API is Open Source, so anyone can run it in its own server.

Also, this very cool **Subgraph** is available: [https://thegraph.com/explorer/subgraph/infinitestyles/dutchx](https://thegraph.com/explorer/subgraph/infinitestyles/dutchx)

## Read only API
The API provides read-only access, because it's not configured with private keys
and is not involved in any transaction signing. 

It just gets the information from the smart contracts.

*Note: The API is provided for information purposes only and reads data from the DutchX trading protocol on the Ethereum Blockchain. We have no control over the transactions executed, attempted to be executed or erroneously executed via the DutchX trading protocol, which is permissionless. We do not give any guarantee that any displayed information is accurate. No assessment or selection is conducted as to the display of the executed, falsely executed or attempted transactions on the DutchX trading protocol. It is possible that this API displays tokens or features that are not compatible with the DutchX trading protocol, because transactions or listings have been made in error. Accordingly, it is not advised to rely on the data displayed on this API to assess the compatibility of an intended transactions with the DutchX trading protocol We do not accept any liability to you or anyone else for any losses of any nature resulting from any transactions made or action taken in reliance on the information contained on this API. All and any such responsibility is expressly disclaimed.*

## Integration with the API
For developers, it should be very easy to get information form the API, check
out these examples:
* [DutchX Example: How to use the API](https://github.com/gnosis/dx-examples-api)   
