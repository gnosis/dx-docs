# Security
Security was the main focus on the design and implementation of the DutchX.

The mechanism is designed to solve the problems various exchanges (centralized
and decentralized ones) face, aiming to remove parties that take advantage and
profit out of the users.

The result is a fair exchange of tokens where all users interact under the same rules.

The smart contracts code was submitted to:

### Internal audit
  * The code is open source and public for anyone to review.
  * During construction, it was subjected to constant internal audits, peer
    reviews, and unit testing.
    
### External audit

  <p align="center">
    <a href="./_static/docs/DutchX_1.0_Audit Report.pdf">
    <img width="150px" src="http://dutchx.readthedocs.io/en/latest/_static/Sol_Badge_SlateOnTrans@2x.png" />
    </a>
  </p>

**DutchX 1.0**

An external audit by three auditors of [Solidified](https://solidified.io/) was conducted.

  * Three auditors reviewed the code in parallel in an isolated review. Then they
    compared the findings and came to a group consensus. After some minor iterations all the risks are mitigated.
  * Check out the <a href="./_static/docs/DutchX_1.0_Audit Report.pdf">Solidify Audit Report</a>.
  * Check this post <a href="https://medium.com/solidified/securing-gnosis-dutch-exchange-smart-contracts-a-case-study-65c3dcc0ed0b" target="_blank">Securing Gnosis’ Dutch exchange smart contracts — a case study</a> to learn more on this audit process.

**DutchX 2.0**

  * Two auditors of Solidified (the same auditors as for the prior audit) reviewed the code.
  * Check out the <a href="./_static/docs/DutchX_2.0_Audit Report.pdf">Solidify Audit Report</a>.
  * Also check out this Solidified [audit report](https://github.com/gnosis/dx-price-oracle/blob/develop/docs/audit_report/Solidified_Audit_Report.pdf) of the [price oracle](https://dutchx.readthedocs.io/en/latest/price-oracle.html)

### Bug bounties
  * On top of the audits, a Bug bounty program was created. It offers generous
    prizes for finding security risks or any other bug.
  * The bug bounty is still ongoing today on the DutchX smart contract code base 2.0 (no bugs have been discovered on DutchX 1.0).
  * Check the details in <a href="https://blog.gnosis.pm/dutchx-smart-contracts-2-0-bug-bounty-861ad756de52" target="_blank">DutchX Smart Contracts 2.0 Bug Bounty</a> for more information.

### Other intgerations
The DutchX is a non-custodial trading protocol. Your funds are only held in
the audited smart contracts, so **no company or organization holds the funds**,
just the audited contracts.  

*Note*: [The dxDAO](https://dutchx.readthedocs.io/en/latest/dxDAO.html) will govern the DutchX. This decentralized autonomous organization may update the master logic of the DutchX with a 30 day time delay. In case of a malicous update, you must: 1) remove your funds from the DutchX smart contracts and 2) revoke any token allowances set! Other than via this update, there is no other connection to the dxDAO. The dxDAO cannot access funds of the DutchX!

*Note*: Keep in mind that, as a user of a decentralized application, you are the only
one who has access to your private key, so it's important that you
**keep you keys safe**.
