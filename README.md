# QBank Ledger Checkpoints

This public repository stores signed QBank ledger checkpoints published by Quorable.

A checkpoint is a small receipt for the QBank ledger. It is not the full ledger and it does not contain readable user IDs. It records the latest ledger fingerprint, transaction count, supply totals, signature, public key, and timestamp.

## Why this exists

QBank stores transactions in a hash-linked ledger. If an old transaction is edited, deleted, reordered, or replaced, the ledger fingerprint changes. Publishing signed checkpoints outside the QBank database makes quiet database rewrites detectable later.

## Files

- `latest.json` is the latest published checkpoint.
- `checkpoints/*.json` keeps the historical checkpoint receipts.

## Verify

Run this from the Game Builder repo:

```bash
npm run verify:qbank -- https://quorable.com
```

The verifier downloads QBank's public proof export, rebuilds the proof chain, checks that the latest checkpoint matches the current chain head, and verifies the Ed25519 signature when a signature is present.

## Publishing

Game Builder publishes here when `QBANK_CHECKPOINT_GITHUB_TOKEN` is configured on the server. The token should only have Contents read/write access to this repository.

Only checkpoint receipts belong in this repository. Do not publish private account data, raw user IDs, auth tokens, or database backups here.
