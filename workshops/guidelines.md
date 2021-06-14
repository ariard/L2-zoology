# Guidelines about L2 protocols onchain security design

## Notes

Multi-party contract protocol (such as LN, Revault, CoinSwap) security models rely on the unilateral
capacity for a contract participant to broadcast transactions aiming to enforce onchain a balance
negotiated off-chain. This security model is actually turning back the double-spend to a private
matter, making the duty of each contract participant to timely enforce its claims against the
competing interest of its counterparties. As such, effective propagation and timely confirmation
of protocol transactions is a critical-safety operation.

However, propagation efficiency is function of the base layer network topology, tx-relay rules,
and mempool acceptance behaviors. Those factors aren't normative in the opposite of consensus rules,
each node is free to define its peer selection strategy, transaction relay mechanism and mempool checks.
This lack of transparency comes at a pitfall for second-layers protocol designers, for inter-compatibility
purposes, transaction format must be well-defined and is actually locked-in in pre-signed transactions.

Beyond, transaction-relay and mempool acceptance rules for L2s don't perfom well under adverserial
settings. Due to the base-layer network being public, a malicious counterparty has an incentive
to meddle with network mempools to steal from the contract (either HTLC, vaulted balance, swapped
output, ...)

The goal of this discussion is to hightlight second-layer security risks w.r.t to transaction
relay rules and mempools behaviors, seek if it's desirable ecosystem-wise to improve support in 
those areas and if positive how to establish a subset of transaction relay rules as a stable API
for second-layers.

## Questions

* What are the security risks of non-propagating transactions for Lightning/L2s ? Beyond transaction-relay jammings and mass panic of channel closures ?
* Can we amend Lightning and other contract protocols to reduce reliance on non-normative rules ? What are the trade-offs ?
* How to increase transparency and stability of tx-relay/mempool acceptance rules across the ecosystem ? Or should L2s deploy their own overlay tx-relay network ? What are the trade-offs ?
* From a second-layer protocol designer viewpoint, how to minimize reliance on tx-relay/mempool acceptance rules while deciding a transaction format ?
* From a base-layer developper viewpoint, should full-node projects adhere to deprecation process when there is a tx-relay/mempool acceptance change affecting downstream projects ?
* What set of "transaction relay" reasonable assumptions a second-layer protocol designer could rely on to draw out a security model ? What the path to realize them in practice ?

## Sources

* [P2P IRC Core meeting on tx-standardness malleability](https://github.com/bitcoin-core/bitcoin-devwiki/wiki/P2P-IRC-meetings#topic-reducing-cve-2020-26895-class-of-bugs-and-tx-standardness-ariard)
* [P2P IRC Core meeting on transaction propagation design goals](https://github.com/bitcoin-core/bitcoin-devwiki/wiki/P2P-IRC-meetings#topic-reducing-cve-2020-26895-class-of-bugs-and-tx-standardness-ariard)
* [Pinning Attacks](https://github.com/t-bast/lightning-docs/blob/master/pinning-attacks.md)
* [add option to bypass contextual timelocks](https://github.com/bitcoin/bitcoin/pull/21413)
* [CVE-2020-26895: LND Low-S Tx-relay Standardness](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002858.html)
* [Non-propagating CL's transactions due to vbyte issue](https://github.com/bitcoin/bitcoin/issues/13283)
* [Non-propagating Electrum's transaction due to min-standard-tx](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2020-May/017883.html)
