# CLI
The Command Line Interface is a very useful tool to trigger smart contract operations such as:
* Get the DutchX account **balance** for any account.
* **Deposit** or **withdraw** funds into/from your DutchX account balance.
* Check the **state** of a given token pair: Auction index, sell/buy volume,
start time, estimated closing time, etc.
* Post a sell order or a buy order.
* Claim back your tokens once the auction has cleared.
* ..and many other useful operations.

It can be used both, in test-nets like `rinkeby`, or in `mainnet`.

The easiest way to use the CLI is to follow the steps described in
[DutchX: CLI scripts and usage](https://github.com/gnosis/dx-cli).

The CLI logic is implemented in the [DutchX Services](https://github.com/gnosis/dx-services),
for more information checkout [DutchX as an open platform](./dutchx-as-an-open-platform.html)

Although the CLI is a very useful tool to do some basic interactions with the
smart contracts, to build tools, bots, or services that interact with the
DutchX, it's a better approach to [Build on top of the DutchX](./dev-truffle.html).
