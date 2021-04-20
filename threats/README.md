This section describes known threats against second-layers protocols.

Most of the threats are classified as instances of transaction-relay jamming, where a counterparty leverage an element of full-nodes transaction and mempool acceptance policy rules to obstruct propagation of
the victim time-sensitive transactions, and thus compromise user's coin safety.

Other classes of attacks are considered, where either the attacker leverage some limitation of the bitcoin system (e.g transaction throughput with [mempools-flooding](mempools-flooding.md) or a privileged role (e.g miner in [miner-harvesting](miner-harvesting.md)). Those latter classes of attacks should deserve more hightlight have they have been less studied from the opinion of this note author.

Bitcoin second-layers are differing in function of their security assumptions and such discussion about different security models is wip in security-models.

Each threat notice describes the vulnerability exploited, one or many attack scenarios, the list of vulnerable protocols, potential mitigations and points toward more ressources.

List of threats:
* [pinning](pinning.md)
* [mempools-flooding](mempools-flooding,md)
* [mempools-partitions](mempools-partitions.md)
* [miner-harvesting](miner-harvesting.md)
* [standardness-malleability](standardness-malleability.md)
* [witness-malleability](witness-malleability.md)

