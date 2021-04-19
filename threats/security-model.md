Bitcoin's second-layer security compromises can be divided into several classes ranging from Channel Jamming Attacks to Time-Dilation Attacks, roughly sorted by layers of abstraction. At the highest, channe
jamming attacks is a family of denial-of-service attacks on LN channels. They're based on a sheer volume of junk payments initiated by the attacker exhausting the liquidity offered by a Lightning node. Even
if they're the subject of much ongoing discussion and research in the Lightning community, we won't cover them in this documentation as they don't rely on exploitation of a base layer primitive. For the same
argument, we'll also exclude from analysis Contract Logic Compromises [^1].

Further, this documentation won't consider for now the lowest known layer exploitable to compromise a L2 security, the block-relay and blockchain view and its associated Time-Dilation/Eclipse class of attacks. Vectors of exploitations are wide and should encompass a discussion of Internet architecture, and some mitigations can be achieved without base layer changes (i.e watchtowers).

This documentation will focus on tx-relay and mempool acceptance layers as those rules directly affect security of most L2s and their reliability have not be considered of high importance by the Bitcoin dev community until recently. Those rules doesn't affect equally Bitcoin L2s and a subset can be dissociated among them, the multi-party contract protocols.

Let's define this class as N participants agreeing on a pre-committed transaction graph swapping coins against goods/services bounded by a time-constraint and initiated by an onchain funding transaction. In this model, the blockchain serves as a judge to arbiter competing claims in case of disagreement about state of the transaction graph. Those claims are materialized by Bitcoin transactions and their validity are subject to time-constraints. As such, contract protocol security model relies on the unilateral capability of a participant to timely confirm onchain one or many transactions, otherwise the contract balance might be captured by the counterparty. TODO: Coinswap example

Due to this time-sensitivity requirement, tx-relay and mempool acceptance rules can be leveraged to compromise integrity of coins employed in such protocols. In comparison, simpler L2 protocols like 
Coinjoin or cut-through don't suffer from the same exploitation severity in case of attacks targetting tx-relay/mempool rules. In the worst-case scenario, participants can take back their coins by
double-spending the negotiated transaction graph, only suffering a timevalue loss.

[^1]: https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002857.html
