.. image:: ./_static/DutchX-logo_blue.svg
    :width: 350px
    :align: center
    :alt: DutchX
    :class: dutchx-logo


The **DutchX** is a fully decentralized trading protocol that
allows **anyone** to add any trading token pair.

It uses the `Dutch auction`_ principle to prevent the problems that other exchanges are experiencing (such
as front running, issues with low liquidity, and third party risk), creating a more fair ecosystem for everyone to use.

There is no restriction besides the fact that tokens must be `ERC20`_
compliant.

Learn more about DutchX
-----------------------
Some interesting links to learn all about the mechanisms of the DutchX are:

* **Small introduction to the features of DutchX**: https://ethresear.ch/t/dutchx-fully-decentralized-auction-based-exchange/2443
* **Blog with information about DutchX**: https://blog.gnosis.pm/tagged/dutchx

Documentation for the Smart Contracts
-------------------------------------
To get a deeper knowledge about the DutchX mechanisms, and the math behind them,
check out the :download:`DutchX Documentation <./_static/docs/DutchX_Documentation.pdf>` for the smart contracts.


.. toctree::
   :maxdepth: 0
   :caption: Documents

   Introduction <self>
   smart-contract-documentation
   dutchx-as-an-open-platform
   market-makers
   api
   cli
   security-of-the-contracts
   contribute

.. toctree::
   :maxdepth: 2
   :caption: Developer guides

   build-on-top-of-dutchx
   use-dutchx-as-an-oracle
   Add a token pair <add-token-pair>
   Run your own bots <run-your-own-bots>

.. toctree::
   :maxdepth: 2
   :caption: Community:
   
   hackathons 
   community-resources
   integration-ideas

.. toctree::
   :maxdepth: 2
   :caption: Reference:

   smart-contracts_addresses
   Github: Smart Contracts <https://github.com/gnosis/dx-contracts>
   Github: Seller Web <https://github.com/gnosis/dx-react>
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
* **Example on using the CLI**: https://github.com/gnosis/dx-cli

Contact the DutchX community
==============================
Find the community in: https://gitter.im/gnosis/DutchX

.. _Dutch auction: https://en.wikipedia.org/wiki/Dutch_auction
.. _ERC20: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md
