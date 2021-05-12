# Full-RBF

## Problem

Currently, to apply the replace-by-fee policy on a transaction, a bip125-compliant mempool will
observe if signaling has been opted-in by the conflicted transaction.

Beyond the pitfalls of the signaling mechanism. this widely-deployed policy on the network opens 
the way of DoS against multi-party funded transactions or even bandwidth-bleeding against full-nodes.
At the same time, zero-conf transactions are still relied on by some merchants and exchanges.

## Question

* what's the list of use cases negatively impacted by opt-in RBF ?
* what's the list of use cases negatively impacted by full-RBF ?
* what are the solutions to improve double-spend of zero-conf txn ?
* how to combine RBF single-tx with RBF package relay ?

## Sources

* [Bandwidth bleeding attacks](https://github.com/bitcoin/bitcoin/pull/16698#issuecomment-571399346)
