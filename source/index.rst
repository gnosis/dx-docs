DutchX's documentation
==================================
The **Dutch Exchange (DutchX)** is a fully decentralized exchange, which
allows **everyone** to add any trading token pair.

It uses the `Dutch auction`_ principle, to prevent the problems that
other exchanges are experiencing (such as front running) getting a
fairer ecosystem for everyone to use.

There is no restriction besides the fact that tokens must be `ERC20`_
compliant.

Learn more about DutchX
-----------------------
Some interesting links to learn all about the mechanisms of the DutchX are:

* **Small introduction to the features of DutchX**: https://ethresear.ch/t/dutchx-fully-decentralized-auction-based-exchange/2443
* **Blog with information about DutchX**: https://blog.gnosis.pm/tagged/dutchx

Documentation for the Smart Contracts
-------------------------------------
To get a deeper knowdedge about the DutchX mechanisms, and the math behind them,
check out the :download:`DutchX Documentation <./_static/docs/DutchX_Documentation.pdf>` for the smart contracts.


.. toctree::
   :hidden:

   Introduction <self>
   smart-contract-documentation
   dutchx-as-an-open-platform

.. toctree::
   :maxdepth: 2
   :caption: Guides:

   First steps (devs) <dev-first-steps>
   Add a token pair <add-token-pair>
   Run your own bots <run-your-own-bots>


.. toctree::
   :maxdepth: 2
   :caption: Reference:
  
   smart-contracts_addresses
   API Reference <https://dx.staging.gnosisdev.com/api>
   Github: Smart Contracts <https://github.com/gnosis/dx-contracts>
   Github: Seller Web <https://github.com/gnosis/dx-react>
   Github: API, Bots, CLI, services <https://github.com/gnosis/dx-services>
   

You may be also interested on
-----------------------------
Related github projects:

* **Smart contracts**: https://github.com/gnosis/dx-contracts
* **Seller interface for DutchX**: https://github.com/gnosis/dx-react
* **Example on using the bots**: https://github.com/gnosis/dx-examples-liquidity-bots
* **Example on using the read API**: https://github.com/gnosis/dx-examples-api
* **Example on using the CLI**: https://github.com/gnosis/dx-example-cli-rinkeby

Contact the DutchX comunity
===========================
Find the comunity in: https://gitter.im/gnosis/DutchX

.. _Dutch auction: https://en.wikipedia.org/wiki/Dutch_auction
.. _ERC20: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md
