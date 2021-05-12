# Coordinated Security Disclosures

## Problem

A serious vulnerability affecting Bitcoin Core transaction relay or mempool acceptance policy and requiring a quick fix might have security implications for deployed second-layers protocols. 

Let's consider the hyptothetical scenario where a security flaw is discovered in the mempool carve-out mechanism such as a memory-DoS crashing full-nodes. Security flaw is reported by an anonymous third-party and as such there is an uncertainty on vulnerability disclosure timeline. Fixing this issue requires knocking out the carve-out mechanism. The bitcoin core dev team proceeds so and invite node operators
to deploy quickly patched full-nodes. Operations of the base layers are safe a priori.

However, the carve-out mechanism is leveraged by Ligthning nodes to protect against a category of pinning attacks. Once patched full-nodes are the majority of the network, Lightning nodes become unsafe and
start to be targeted by attackers. Beyond, Lightning nodes operators might rattle and manually close their channels, congestioning the mempools for a significant number of blocks. As a fireback, operations
of the base layer are disrupted by a sudden influx of high-feerate lightning transactions. Normal transactions don't confirm for a while.

A more optimistic scenario to envisage would be coordination across-layers where downstream projects dev team would be able to patch their protocols and deploy them to minimize security risks on their users.

CVE-2021-31876, though we benign security implications, provided an interesting fire-and-drill case. Bitcoin Core implementation of BIP125 was not matching with the specification, thus making some pinning
attacks cheaper against LN nodes. In the meantimes, a new channel type, "anchor" is mitigating against the issue by forcing RBF signaling on all channel transactions. If LN already have a upgrade mechanism,
not involving a new onchain transaction, LN operators could have migrate vulnerable channels to a safer ones.


## Questions

* in case of base layer security issues, how to identify L2 protocols affected ?
* how to communicate promptly to L2 projects maintainers ?
* should Core and other full-nodes implementations have downstream projects security bulletins/advisories ?
* should any L2 protocol have an emergency upgrade mechanism to avoid massive onchain closing ?
* in case of incompatible fixes across-layers, how to minimize the windblow ?

## Sources

* [Dynamic Commitments: Upgrading Channels Without On-Chain Transactions](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-July/002763.html)
* [CFPP-Carve-out](https://bitcoinops.org/en/topics/cpfp-carve-out/)
* [CVE-2021-31876](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2021-May/018893.html)
* [Dynamic Upgrades](dynamic-upgrades.md)
