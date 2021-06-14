# Guidelines about coordinated cross-layers security disclosures

## Notes

Mitigating a security issue around tx-relay or the mempool in Bitcoin Core or any other full-node
implementation might have harmful implications for downstream projects. For e.g, a DoS vector
might be found in the mempool forcing base-layer protocol to break a feature to reduce the attack
surface. In the meantime, this feature might be relied on by some second-layer protocols.

CVE-2021-31876 was a concrete instance of such concern. For context, the Core's mempool didn't
perfectly adhere to the BIP125 specification. This defects did break some L2 protocol (e.g blind
merge mining) or downgrades security of others (e.g LN's pinning attack at the htlc-level).

Further, LN did have a type of channel mitigating against this issue, if dynamic upgrades have been already
deployed and the security risk more serious, an emergency upgrade of the LN ecosystem could have
been realized, without massive onchain channel closure.

## Questions

* In case of transaction relay wreckage at the base layer, how to identify L2 protocols affected ?
* How to enable prompt communication from base-layer maintainers to L2 downstream project maintainers ?
* Should Bitcoin Core and other full-nodes implementation have security bulletins for downstream projects ?
* How to promote dynamic upgrades across the L2s ecosystem as a standard security mechanism ?
* In case of incompatible fixes across layers, how to minimize the windblow ?

## Sources

* [CVE-2021-3187 Defect in Bitcoin Core's bip125 logic](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2021-May/018893.html)
* [Dynamic Commitments: Upgrading Channels without On-Chain Transactions](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-July/002763.html)
