# Security
Security was the main focus on the design and implementation of the DutchX.

The mechanism are desing to solve the problems of other exchanges (centralized 
and not centralized ones) so there are not parties taking advantage and 
profiting out of the users. The result is a fare echange of tokens were all 
users play under the same rules.

The smart contract's code was submited to:
* Constant internal audits within it's construction
* A thourough external audit by Solidify ([https://solidified.io/](https://solidified.io/))
  * Several auditors review the code in paralel in an isolated review. Then they
    compare the findings and come to a group consensus. Then the final report
    is done, and over some iterations all the risks are mitigated.
  * Check out the <a hred="./_static/docs/Solidified_Audit_Report.pdf">Solidify Audit Report</a>.
  * Check this post to learn how was the proccess: 
  [https://medium.com/solidified/securing-gnosis-dutch-exchange-smart-contracts-a-case-study-65c3dcc0ed0b](https://medium.com/solidified/securing-gnosis-dutch-exchange-smart-contracts-a-case-study-65c3dcc0ed0b)

The DutchX is a non-custodial trading protocol.
Your funds are only ever held in audited smart contracts.

There still is a public bug bounty running and no bugs have been discovered.

As a user in the decentralized applications, and for DutchX in particular, you 
are the only one who has access to your private key, so it's imporant that
you **keep you keys safe**.

