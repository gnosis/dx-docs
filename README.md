<p align="center">
  <img width="350px" src="http://dutchx.readthedocs.io/en/latest/_static/DutchX-logo_blue.svg" />
</p>

# DutchX Documentation
The **DutchX** is a fully decentralized trading protocol, which allows
**anyone** to add any trading token pair.

It uses the **[Dutch auction](https://en.wikipedia.org/wiki/Dutch_auction)**
principle to prevent the problems that other exchanges are experiencing (such
as front running, low volume trading, and third party risk), creating a more fair ecosystem for everyone to use.

There is no restriction besides the fact that tokens must be
[ERC20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md) compliant.

## Documentation
Read the last documentation in:
* [http://dutchx.readthedocs.io/en/latest/](http://dutchx.readthedocs.io/en/latest/)

This is a work in progress, so comments, suggestions, and collaborations are more than
welcome.

## Collaboration
The DutchX is made by and for the community, with the goal of having a more fair standard
to exchange any kind of token.

Meet the community in our Gitter channel!
* https://gitter.im/gnosis/DutchX

# Generate the doc
```bash
pip3 install -r requirements.txt
make html
```
