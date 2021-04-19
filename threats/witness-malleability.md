# Witness Malleability

## Vulnerability

A transaction witness might be inflated by a malicious participant to decrease the overall transaction
feerate thus making the transaction stuck in the mempool. Within a witnessScript wit alternatives
branches, the most-expensive one can be used instead of the cheapest one when satisfying solutions
for both are known.

TODO: Miniscript documentation mentions it

## Attack

## Vulnerable Protocols

Any multi-party funded protocol :
- DLC
- dual-funded LN
- coinjoin
- 

## Mitigations

