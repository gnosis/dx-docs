# DutchX as an open platform
DutchX it's **100% open source** and it's been build as a community effort to improve
the problems inherit from centralised platforms or other decentralised ones.

DutchX is an ecosystem of interfaces, on chain apps, and smart contracts that
create a common liquidity pool that all users can benefit from.

![Open Platform](./_static/open-platform.png)

## Smart contracts
The core of the project is the Smart Contracts, that hold the logic described in
the [Smart Contract Documentation](./smart-contract-documentation.html), and
can be found in [https://github.com/gnosis/dx-contracts](https://github.com/gnosis/dx-contracts)

The smart contracts is the base of this open platform, and anyone can build
tools, applications and interfaces on top of them, making the DutchX a unique
fair protocol to exchange tokens.

The main contract are:
* [**DutchExchange.sol**](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchange.sol):
The one holding all the Dutch Auction mechanisms. It will have for example the
logic for adding a new token pair, posting a sell order or a buy order.
* [**DutchExchangeProxy.sol**](https://github.com/gnosis/dx-contracts/blob/master/contracts/DutchExchangeProxy.sol):
The contract that act as an intermediary between the users and the core contract.
This contract is the one holding the data of the DutchX, so it's the one we should
use to interact with the DutchX. Please, read more about the Proxy Pattern for
Smart Contracts in this <a href="https://blog.gnosis.pm/solidity-delegateproxy-contracts-e09957d0f201" target="_blank">Solidity DelegateProxy</a> post.

Security was the main focus on the design and implementation of the DutchX.
Check out the [Security in DutchX](./security-of-the-contracts.html).

## Services, API, Bots and CLI
Another important piece on the DutchX is the [DutchX services](https://github.com/gnosis/dx-services) project.

This project uses the smart contract as a base layer, and build some
 repositories, services and utilities on top of it.

This project may be split into different smaller ones in the future.

It has the following parts:
* **Repositories**: Abstraction on top of the smart contracts to make it easier
to interact with them. For example, they add the same validations that are going
to be performed in the smart contract, so they can throw more meaningful errors,
instead of the `revert` that smart contracts throw.
* **Services**: Some use cases built on top of the DutchX. The CLI, Bots and API
 use this layer to perform all it's tasks.
* **API**: REST Api that provides a simpler access to the data in the DutchX.
Check out the [API documentation](./api.html)
* **CLI**: The Command Line Interface it's a very useful tool for invoking some
operations in the smart contracts such as posting sell/buy orders, and to
extract some information from them (for example getting the status of a token
pair).
It can be used in test nets like `rinkeby` or in `mainnet`.
Learn more about the [CLI](./cli.html) page.
* **Bots**: The bots are series of small applications that run in the background
and have a scoped task to fulfil. They interact with the DutchX performing some
operations. For example the liquidity bots watch some markets and provide
liquidity ensuring the auctions run continuously and the prices don't drop below
market price. Learn more about the bots in the guide.
[Run your own bots](./run-your-own-bots.html)

## Seller interface
The seller interface is a nice interface that allows users to participate in the
auctions in a simple way. It can be found in [https://github.com/gnosis/dx-react](https://github.com/gnosis/dx-react).

For using it, you just need to install the [Metamask](https://metamask.io/)
plugin. Of course you will also need to hold the tokens you want to trade in
that account.

Checkout the [**DutchX Web DEMO in Rinkeby**](https://dutchx-rinkeby.d.exchange/).

This interface can be used by anyone as a base to build alternative ones, a
buyer interface, or just host it in any server. So feel free to contribute to
the DutchX ecosystem.

## Contribute
The community is what makes DutchX great.

Became part of it and contribute to create new interfaces, improve the tools,
and spread the word.

Meet the community in Github and the [Gitter channel](https://gitter.im/gnosis/DutchX).
