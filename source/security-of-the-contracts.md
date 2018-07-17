# Security
Security was the main focus on the design and implementation of the DutchX.

The mechanism are desing to solve the problems of other exchanges (centralized 
and not centralized ones) so there are not parties taking advantage and 
profiting out of the users.

The result is a fare echange of tokens were all users play under the same rules.

The smart contract's code was submited to:
* **Internal audits**:
  * The code is open source and public for anyone to review.
  * During the construction, it was subjected to constant internal audits 
    peer reviews, and unit testing.
* **External audit**: A thourough external audit by Solidify ([https://solidified.io/](https://solidified.io/))
  * Three auditors reviewed the code in parallel in an isolated review. Then they
    compare the findings and come to a group consensus. Then the final report
    is done, and over some iterations all the risks are mitigated.
  * Check out the <a hred="./_static/docs/Solidified_Audit_Report.pdf">Solidify Audit Report</a>.
  * Check this post <a hred="https://medium.com/solidified/securing-gnosis-dutch-exchange-smart-contracts-a-case-study-65c3dcc0ed0b" target="_blank">Securing Gnosis’ Dutch exchange smart contracts — a case study</a> to learn how was the proccess.
  
* **Bug bounty**:
  * As suggested by the auditors, it was created a Bug bounty program with 
    genereous prizes for finding bugs and specially security risks.
  * Check the post <a hred="https://blog.gnosis.pm/gnosis-dutchx-and-initial-owl-generation-bug-bounty-71ba53dfd2db" target="_blank">Gnosis DutchX and Initial OWL Generation Bug Bounty</a> for more information.

The DutchX is a non-custodial trading protocol. Your funds are only held in 
the audited smart contracts.

There still is a public bug bounty running and no bugs have been discovered.

As a user in the decentralized applications, and for DutchX in particular, you 
are the only one who has access to your private key, so it's imporant that
you **keep you keys safe**.

