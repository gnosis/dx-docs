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

## Read only API
The API provides read-only access, because it's not configured with private keys
and is not involved in any transaction signing. 

It just gets the information from the smart contracts.

## Integration with the API
For developers, it should be very easy to get information form the API, check
out these examples:
* [DutchX Example: How to use the API](https://github.com/gnosis/dx-examples-api)   
