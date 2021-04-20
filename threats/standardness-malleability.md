# Standardness Malleability

## Vulnerability

Base layer node incorporate a number of non-normative, non-consensus rules affecting transactions
relay either to mitigate against bandwidth/CPU/memory DoS or favor some behaviors on the p2p network.
This set of rules varies across node implementations, software versions and might be configured by
node operators. For e.g, in Bitcoin Core, `MAX_STANDARD_TX_WEIGHT` enforces a upper bound on size of 
transactions relayed or `DUST_RELAY_TX_FEE` serves as base to determine the minimal amount size an
output must create. TODO: compare to bitcoin consensus rules limits.

In some L2 protocols, transactions are cooperatively built by participants. They contribute to a
number of transactions parameters, such as outputs, inputs, witnesses, feerate, timelocks, etc.

Any such malleable parameter can serve as a standardness invalidity injection vector by an attacker and
thus lead the victim to own effectively non-relayable transactions.

## Attack

## Vulnerable Protocols

* Lightning, contract balance integrity
* Coinswap ?
* Vaults ?
* DLC ?

## Mitigations


TODO: incorporate p2p meetings discussions
TODO: CVE-2020-26895
