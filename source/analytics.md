# Analytics & Alerts

Where can you gather information on what's happening on the DutchX Protocol Level on the Ethereum blockchain?

There are some sources available for you:

1. Check out the [**read-API**](https://dutchx.readthedocs.io/en/latest/api.html)
2. Check out the [**Subgraph**](https://thegraph.com/explorer/subgraph/infinitestyles/dutchx)
3. Check out this [**dashboard**](https://explore.duneanalytics.com/public/dashboards/nigajDs8cp1lkmoXYNgdo3jMh2XCzUIiLk0J5Fst) provided by [Dune Analytics](https://www.duneanalytics.com/) 

You can also create your own alert on [**Alethio Monitoring**](https://company.aleth.io/blockchain-monitoring) to get notified of certain events on the DutchX. As an example, below is a step-by-step guide for an alert that tracks the event of a new token being added to the DutchX.
- Select to monitor **Smart Contracts**
- Add the contract address of the DutchX proxy contract: **0xb9812e2fa995ec53b5b6df34d21f9304762c5497**
- Filter for both transactions and contract messages (internal transactions)
- Filter for the payload prefix (method ID), in case of the addTokenPair function this is **0xe9f8cd70**
- To get notified every time the the addTokenPair function is called, set the trigger criteria to a **1% increase** within **5 min**
- Choose your prefered notification channel (currently only slack & email available)
