Hi,

During the lastest years, tx-relay and mempool acceptances rules of the
base layer have been sources of major security and operational concerns for
Lightning and other Bitcoin second-layers [0]. I think those areas require
significant improvements to ease design and deployment of higher Bitcoin
layers and I believe this opinion is shared among the L2 dev community. In
order to make advancements, it has been discussed a few times in the last
months to organize in-person workshops to discuss those issues with the
presence of both L1/L2 devs to make exchange fruitful.

Unfortunately, I don't think we'll be able to organize such in-person
workshops this year (because you know travel is hard those days...) As a
substitution, I'm proposing a series of one or more irc meetings. That
said, this substitution has the happy benefit to gather far more folks
interested by those issues that you can fit in a room.

# Scope

I would like to propose the following 4 items as topics of discussion.

1) Package relay design or another generic L2 fee-bumping primitive like
sponsorship [0]. IMHO, this primitive should at least solve mempools spikes
making obsolete propagation of transactions with pre-signed feerate, solve
pinning attacks compromising Lightning/multi-party contract protocol
safety, offer an usable and stable API to L2 software stack, stay
compatible with miner and full-node operators incentives and obviously
minimize CPU/memory DoS vectors.

2) Deprecation of opt-in RBF toward full-rbf. Opt-in RBF makes it trivial
for an attacker to partition network mempools in divergent subsets and from
then launch advanced security or privacy attacks against a Lightning node.
Note, it might also be a concern for bandwidth bleeding attacks against L1
nodes.

3) Guidelines about coordinated cross-layers security disclosures.
Mitigating a security issue around tx-relay or the mempool in Core might
have harmful implications for downstream projects. Ideally, L2 projects
maintainers should be ready to upgrade their protocols in emergency in
coordination with base layers developers.

4) Guidelines about L2 protocols onchain security design. Currently
deployed like Lightning are making a bunch of assumptions on tx-relay and
mempool acceptances rules. Those rules are non-normative, non-reliable and
lack documentation. Further, they're devoid of tooling to enforce them at
runtime [2]. IMHO, it could be preferable to identify a subset of them on
which second-layers protocols can do assumptions without encroaching too
much on nodes's policy realm or making the base layer development in those
areas too cumbersome.

I'm aware that some folks are interested in other topics such as extension
of Core's mempools package limits or better pricing of RBF replacement. So
l propose a 2-week concertation period to submit other topics related to
tx-relay or mempools improvements towards L2s before to propose a finalized
scope and agenda.

# Goals

1) Reaching technical consensus.
2) Reaching technical consensus, before seeking community consensus as it
likely has ecosystem-wide implications.
3) Establishing a security incident response policy which can be applied by
dev teams in the future.
4) Establishing a philosophy design and associated documentations (BIPs,
best practices, ...)

# Timeline

2021-04-23: Start of concertation period
2021-05-07: End of concertation period
2021-05-10: Proposition of workshop agenda and schedule
late 2021-05/2021-06: IRC meetings

As the problem space is savagely wide, I've started a collection of
documents to assist this workshop : https://github.com/ariard/L2-zoology
Still wip, but I'll have them in a good shape at agenda publication, with
reading suggestions and open questions to structure discussions.
Also working on transaction pinning and mempool partitions attacks
simulations.

If L2s security/p2p/mempool is your jam, feel free to get involved :)

Cheers,
Antoine

[0] For e.g see optech section on transaction pinning attacks : https://bitcoinops.org/en/topics/transaction-pinning/
[1] https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2020-September/018168.html
[2] Lack of reference tooling make it easier to have bug slip in like : https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002858.html
