# Lightning, Yet An Extra Little Bit Of Trust

YAELBOT allows opening a channel with a trusted peer simply by setting up
a multi-sig 2of2 (but not just a one-time address, but rather an unlimited
[Electrum Bitcoin Wallet-like][e2of2] wallet which allows movement at
any time) and then informing the node about a mutually-signed state
of channel.

[e2of2]: https://electrum.readthedocs.io/en/latest/multisig.html

Imagine a slower, human-understanding-friendly [manual transmission][mt]
equivalent to the current fully-automated channel. No automatic fee
discovery or anything else can close the channel without the two parties
mutually agreeing on closing it.

[mt]: https://en.wikipedia.org/wiki/Manual_transmission

Any other Lightning Network node can verify the YAELBOT channel contains
the funds by using public keys of both channel sides. Example:

 1. Set up a multi-sig wallet.
 2. Fund it.
 3. Sign a message about channel state with the other party.
 4. Use the signed message to tell your Lightning Network
    node about the channel.
 5. The node starts gossiping about it.

All the fee and other negotiations are handed-over to humans. Changes
(funds added or removed) can be broadcast anytime both ends of the channel
mutually agree on them, possibly as a new Lightning Network channel,
but on the L1 it would be the same old UTXOs plus new ones if the funds
are merely added.
