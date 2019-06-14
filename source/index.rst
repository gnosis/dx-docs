.. image:: ./_static/DutchX-logo_blue.svg
    :width: 350px
    :align: center
    :alt: DutchX
    :class: dutchx-logo


The **DutchX** is a fully decentralized trading protocol that
allows **anyone** to add any trading token pair.

It uses the `Dutch auction`_ principle to prevent the problems that exchanges are experiencing (such
as front running, issues with low liquidity, and third party risk), thereby creating a more fair ecosystem for everyone to use.

There is no restriction besides the fact that tokens traded on the DutchX must be `ERC20`_
compliant.

.. raw:: html

    <div style="position: relative; padding-bottom: 6.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
       <iframe width="560" height="315" src="https://www.youtube.com/embed/_TBVXT6XIe0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div> 

Learn more about DutchX
-----------------------
Here are some interesting links to learn all about the mechanisms of the DutchX:

* **Small introduction to the features of DutchX**: https://ethresear.ch/t/dutchx-fully-decentralized-auction-based-exchange/2443
* **Blog with information about DutchX**: https://blog.gnosis.pm/tagged/dutchx

Documentation for the Smart Contracts
-------------------------------------
To get a deeper knowledge about the DutchX mechanisms, and the math behind them,
check out the :download:`DutchX Documentation <./_static/docs/DutchX_Documentation.pdf>` for the smart contracts.


.. toctree::
   :maxdepth: 0
   :caption: Documents:

   Introduction <self>
   Mechanism <mechanism>
   smart-contract-documentation
   Price Oracle <price-oracle>
   List a token to trade <add-token-to-trade>
   dutchx-as-an-open-protocol
   The dxDAO <dxDAO>
   market-makers
   Interfaces <interfaces>
   Pooling for MGN <ERC20-pool-for-MGN>
   api
   cli
   analytics

.. toctree::
   :maxdepth: 0
   :caption: Developer guides:

   Get started: Build on top of DutchX <dev-get-started>
   Local development + truffle <dev-truffle>
   On-chain integration <dev-onchain-oracle>
   Deposit tokens <dev-deposit>
   Add a token pair <add-token-pair>
   Bots: Automated minimal liquidity <bots-market-making>
   Bots: Types <bots-types>
   Bots: Security <bots-security>
   Bots: Add a price feed for the bots <bots-price-feed>
   Bots: Arbitrage to Uniswap <uniswap-arbitrage>

.. toctree::
   :maxdepth: 2
   :caption: Community:

   hackathons
   community-resources
   integration-ideas
   contribute

.. toctree::
   :maxdepth: 2
   :caption: Reference:

   smart-contracts_addresses
   security-of-the-contracts
   Github: Smart Contracts <https://github.com/gnosis/dx-contracts>
   Github: API, Bots, CLI, services <https://github.com/gnosis/dx-services>


Related Github projects
-----------------------------

* **Smart contracts**: https://github.com/gnosis/dx-contracts
* **Seller interface for DutchX**: https://github.com/gnosis/dx-react
* **Services, API, Bots and CLI**: https://github.com/gnosis/dx-services

**Examples and guides**:
* **Examples on how to build on top of the DutchX**: https://github.com/gnosis/dx-examples-dev
* **Example on using the bots**: https://github.com/gnosis/dx-examples-liquidity-bots
* **Example on using the read API**: https://github.com/gnosis/dx-examples-api
* **Example on using the CLI**: https://github.com/gnosis/dx-tools

Contact the DutchX community
==============================
Find the community in: https://gitter.im/gnosis/DutchX

.. _Dutch auction: https://en.wikipedia.org/wiki/Dutch_auction
.. _ERC20: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md
