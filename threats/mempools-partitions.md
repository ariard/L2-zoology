# Mempool Partitions

## Vulnerability

Bitcoin network p2p and mempool acceptance rules are racy, in the sense of the local order of events determines the next events accepted. For e.g, Alice observes tx X, tx Y and tx Z and Bob observes tx Z, 
tx X and tx Y. Tx X and Tx Z are spending the same utxo. Both transactions are offering the same feerate. Following BIP 125 rules, a replacement of X by Z or vice versa will failed. Alice's mempool contains
tx X and tx Y. Bob's mempool contains tx Z and Y. If a subsequent child of tx X offers a high-fee, Alice and Bob will start to observe different mempools feerate. 

Beyond opt-in RBF as described by bip25, potentially any p2p/mempool acceptances rules can provoke a divergence acrosss network mempools. That said, bip125 deserves specific awareness as it's widely deployed
on the network and as such could be exploited by attackers to provoke mempools partitions at scale, without having to probe each node to fingerprint its policy. An active attackers can massively connect to 
a multitude of honest nodes and partition network mempools in different subsets by simply announcing opt-out rbf transactions (`nSequence` = 0xffffffff).

## Attacks

### Propagation Obstruction of Time-Sensitive Transactions

From _Pinning : The Good, The Bad, The Ugly_, TODO: to be reworked

"
Let's assume the following base layer tx-relay topology:

                Alice ---> Bob ---> Caroll

Alice wants to send her package relay to Caroll the miner to get her commitment transaction confirmed. A malicious counterparty could throw remote commitment W in Bob mempool and remote commitment X in
Caroll mempool. Transaction W would be attached to a high-fee CPFP Y. Transaction X would be attached to a low-fee CPFP Z such that X pins in Caroll mempool. CPFP Y and CPFP Z would be crafted such as both
incorporating a conflicting parent to prevent Bob and Caroll mempool convergence. It looks like the following:

Bob's mempool:
tx W ---> tx Y
parent 1 ---> tx Y

Caroll's mempool:
tx X ---> tx Z
parent 2 ---> tx Z

Bob's mempool would announce and send package "tx W + tx Y + parent 1" to Caroll's one and due to parent 1 and parent 2 spending the same output package would be rejected. High-fee package W will prevent
Alice to successfully broadcast her package to Caroll. This fee can be higher than the maximum one that Alice would pay to confirm her transaction, as due to conflicts, it won't be _effectively_ paid by
the malicious counterparty.

This scenario does bear a risk to the attacker only if miner mempools haven't been well-mapped and high-fee package leak into them, is hard to execute but has a likely double-digit rate of success. It
assumes mempool partitions, network topology knowledge and inter-layer mapping"

### Mempool-Spoofing against LN Node


### Bandwidth-Bleeding of Rebroadcasting Node


## Vulnerable Protocols

User coin's safety risks
* Lightning
* DLC
* Coinswap
* vaults

## Mitigations

### Full-RBF

### Outbound tx-relay peers rotation

## Sources

* [Bandwidth Bleeding Concerns against Full-Nodes](https://github.com/bitcoin/bitcoin/pull/16698#issuecomment-571399346)
* [Pinning : The Good, The Bad, The Ugly](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-June/002758.html)
* [TxProbe: Discovering Bitcoin's Network Topology Using Orphan Transactions](https://arxiv.org/pdf/1812.00942.pdf)
