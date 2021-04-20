# Transaction Pinnings

## Vulnerability

* describe mempool package limits as a vector

* describe rbf rule #3

## Attacks 

### Pinnings of Concurrent Transactions

From _Pinning : The Good, The Bad, The Ugly_, TODO: to be reworked

"As Matt previously explained in his original mail on RBF-pinning, a malicious counterparty has an interest to pin a low-feerate HTLC-preimage transaction in some network mempools and thus preventing a
honest HTLC-timeout to confirm. For details, refer to Optech newsletter [2].

This scenario doesn't bear any risk to the attacker, is easy to execute and has double-digit rate of success. You don't assume network topologies manipulation, mempools partitions or LN-node-to-full-node mapping [3] That said this should be solved by implementing and deploying anchor outputs, which effectively allows a party to unilaterally bump feerate of its HTLC-timeout transactions"

### Pinnings of State Transactions

"Digging further, we found that there are more concerning scenarios of pinning, at the commitment-tx level. At a period of low-feerate, a malicious party incessantly updates a channel until to obtain ~10k
revoked commitment transactions.

At a period of mempool-congestion, by having setup a fine-grained `dust_limit_satoshis` and at same-time circulary routing HTLCs, our malicious party can inflate absolute fee of its own commitment bounded
while breaking channel in the middle of an update sequence, ensuring it has a higher-fee than the commitment of the honest counterparty. As channel opener, the attacker has the amplitude of malleating the
victim's commitment such to keep it equal or under revoked feerate.

Then our malicious party broadcast to each base layer public peer one of the revoked commitment transactions, that way partitioning the network mempools in 10k subset. Even assuming anchor output a honest
LN node won't be able to confirm the remote commitment through a CPFP, this one failing to cross subset boundaries, the parent txid being different at each.

Broadcasting the honest commitment transaction will fail, its feerate being known and malleable it won't RBF already-in-mempool remote commitment transactions. This prevents an honest party to timely timeoutan outgoing HTLC or an incoming HTLC.

This scenario does bear a low-risk to the attacker, is easy to execute and has a likely double-digit rate of success once you tune feerate malleability. You assume mempools partitions but not any network
topologies discovery. We underscore there is no current p2p/mempool mechanism to learn about conflicting transactions, even learning about near-topology conflicts don't guarantee you that a propagation
path is uniform to make your CPFP successful."

### Timevalue DoS

TODO

### Pinning of State Transactions

## Vulnerable Protocols

## Mitigations

### Anchor Output

### Full-RBF

### Package-Relay

### NO_INPUT-bumping

## Sources

* [RBF Pinning with Counterparties and Competing Interest](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-April/002639.html)
* [Pinning : The Good, The Bad, The Ugly](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-June/002758.html)
