# Limits

These are properties of the testnet, not missing pages in this document.

- Amounts are public. An observer can see how much TIC moved.
- Fees are public.
- The note graph is public. A commitment in an input is the note that was spent. A nullifier is published beside it.
- The sender of a note learns the one-time key, because the sender generated it. Sweep is what removes that key's power.
- Block proposers are public ML-DSA keys.
- A contract capability key is public on every call it authorizes.
- There is no peer-to-peer network in this version, so network-level privacy is outside the protocol.
- The implementation is not audited.
- There is no mainnet parameter set. Genesis uses `timecoin-testnet.genesis.v1` so these blocks cannot be replayed onto a later network by accident.

The privacy claim stops at the list in the README. A note amount is not hidden. A memo is hidden from every key except the recipient view key. Both sentences are enforced by the same code.
