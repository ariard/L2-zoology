# Package-Relay & Friends

Package-relay has been in discussion among the Bitcoin development community since at least 2018.
Initially proposed as a mechanism to improve feerate of small network mempools (< default settings),
it has been also proposed as a fee-bumping primitive to support Lightning and second-layers protocols
(see "Package relay design questions" opener).

More recently since last year, it has been pointed to multiple times to solve few vectors of
transaction pinnings against legacy and anchor LN channels. At least two classes of pinnings
exist against Lightning, at the transaction-level and at the commitment-level. If the ones
at the transaction-level are solved by upgrading to anchor LN channel, we still have the
remaining case of commitment-level transaction where a transaction might see its propagation
blocked by a higher-absolute-fee/lower-feerate transaction (see "Pinning : The Good, The Bad,
The Ugly", scenario 2a/2b). Are those attack serious enough and if so what's the array of solutions ?

Another discussion would be the design of an enhanced fee-bumping primitive to support multi-party,
scalable protocols. Few designs have been sketched out so far (sponsorship, newer malleability flags,
transaction mutation scheme).

# Questions

* what problem(s) package-relay aim to solve at the base-layer ? E.g CPFP fee-bumping issue with small mempools/malicious mempool partitions ?
* what problem(s) package-relay aim to solve for second-layers ? Pre-signed feerate, tx-pinning ?
* are the problems shared to every second-layers or each of them has specific requirements ?
* do we have an interdependency w.r.t to solving them ?
* what are the different solutions to solve pre-signed feerate ? what are the trade-offs offered in term of feerate perfomance/key management/bandwidth/...?
* what are the different solutions to solve tx-pinnings ? what's the challenges to any mempool re-design ?
* how L2s behavior might influence package-relay design w.r.t to bandwidth consumptions/package format ?
* any feedback if a specification would help to implement package-relay support in their backend ?
* what's package-relay/anchor output limitations/benefits w.r.t to multi-party protocols ?

## Sources

* [Package relay design questions](https://github.com/bitcoin/bitcoin/issues/14895)
* [Receiver-initiated PoC](https://github.com/bitcoin/bitcoin/pull/16401)
* [Sender-initiated PoC](https://github.com/bitcoin/bitcoin/pull/19621)
* [Waiting SIGHASH_ANYPREVOUT and Packing Packages](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2021-June/019084.html)
