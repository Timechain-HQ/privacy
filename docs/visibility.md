# Visibility

A full node stores every accepted block and re-executes it. Privacy is whatever that record does not contain. It is not a filter applied after the fact.

## Note

The commitment binds the public amount, the one-time ML-DSA-44 public key, the 32-byte rho, the ML-KEM-768 ciphertext, the cipher, and the MAC. The domain string is `timecoin.note.v1`.

The nullifier is derived from the one-time public key and rho. The domain string is `timecoin.null.v1`. Publishing it marks the note spent. It does not reveal the view key.

The plaintext inside the cipher starts with `TN1` and carries the amount, rho, the one-time private key, and the memo. The amount inside the plaintext has to match the public amount. The MAC is HMAC-SHA256 over the ciphertext, keyed by the ML-KEM shared secret. A wrong view key fails the MAC. ML-KEM decapsulation still returns 32 bytes on a mismatch, so the MAC is the check that matters.

## Transaction

A transfer signs its sighash with each one-time spend key. The sighash domain is `timecoin.sighash.v1`. The signature proves the right to spend that note. It does not name a long-term account.

A contract call adds the contract id, the arguments, the call value, and a signature from the contract capability key. The capability key is public on that call. It is not the view key.

## Block

The proposer public key is on the block. The coinbase is an ordinary note: its amount is the 50 TIC reward plus the fees, and its payload is sealed to the payee's view key. Uncle transactions are not executed, so an uncle does not publish a second copy of those notes onto the canonical state.

## Supply

Unspent note amounts plus contract TIC balances equal `state.supply` after every block. Supply increases only by the 50 TIC reward. Fees move into the coinbase. A node that drops this check is not running the testnet.
