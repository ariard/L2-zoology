# L2 Support Philosopy

## Problem

Multi-party contract protocols security models rely on the unilateral capability for a contract participant to confirm transactions before reaching out a negotiated timelock expiration. Failure to timely
confirm a transaction opens the way for the counterparty to compitevely claim a disputed utxo. Ensuring effective propagation and timely confirmation of a time-sensitive transaction (e.g a HTLC-timeout)
is so a critical-safety operation. 

This security model is making a set of assumptions on base layer's transaction relay and mempool acceptances rules. For e.g, pre-signed transactions outputs must be above the full-node's dust limit. In
case of a sudden bump of the dust limit among a majority of the network nodes, all those pre-signed transactions would become ineffective to propagate. However, those rules have always been considered
as non-reliable, non-normative and racy by base layer developpers and operators.

Pursuing the current L2 design practice of relying on non-normative rules for protocol safety increas the odds of security failures due to lack of rules verification (cf. CVE-2020-26895). On the other side, carrying on to make those rules more reliable might not be incentivized-compatible, slow down development in those areas or effectively reduce node's area of policy.

## Questions
* could we redesign L2's security models to minimize reliance on tx-relay/mempool acceptance rules ?
* from a l2 dev viewpoint, how to decide the format of my transactions (size, scripts, witness, minimal fee, ...) ?
* from a l2 dev viewpoint, how to pick up a rebroadcast/fee-bumping strategy ?
* should full-node implementations transaction relay policy be more documented ?
* should full-node implementations offer tooling to verify transaction compliance to its relay policy ?


## Sources
* [CVE-2020-26895: LND Low-S Tx-relay Standardness](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002858.html)
* [P2P IRC Meeting 1](http://gnusha.org/bitcoin-core-dev/2020-09-22.log)
* [P2P IRC Meeting 2](http://gnusha.org/bitcoin-core-dev/2020-11-17.log)
* [P2P IRC Meeting 3](http://gnusha.org/bitcoin-core-dev/2021-04-20.log)
* [add option to bypass contextual timelocks in testmempoolaccept](https://github.com/bitcoin/bitcoin/pull/21413)
