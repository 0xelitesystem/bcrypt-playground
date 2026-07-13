# bcrypt playground

An educational, fully client-side bcrypt playground. Generate and verify bcrypt hashes, inspect the anatomy of a hash string, and learn why bcrypt is the right tool for password storage. Everything runs in your browser with no external dependencies.

## Live demo

https://0xelitesystem.github.io/bcrypt-playground/

## Features

- Password input with a live cost slider (4 to 15) and a "slower is heavier" warning as the work factor climbs.
- `$2a$` / `$2b$` version toggle.
- One-click hash generation using a per-hash random 128-bit salt.
- Labelled hash anatomy that colour-codes the prefix, cost, 22-character salt, and 31-character digest.
- A verify panel that reports MATCH or NO MATCH for a password against any bcrypt hash.
- A short "why bcrypt" section covering work factor, salting, and adaptivity.

## How it works

The bcrypt (Eksblowfish) algorithm is implemented from scratch in plain JavaScript, inline in `index.html`. There is no build step and there are no libraries to install. The implementation:

- Runs the expensive key schedule `2^cost` times, exactly like OpenBSD's `crypt_blowfish`, so its output is interoperable with standard bcrypt vectors.
- Draws salt bytes from `crypto.getRandomValues`.
- Encodes salt and digest with bcrypt's own base64 alphabet.
- Compares digests with a constant-time-style loop during verification.

Just open `index.html` in any modern browser. It is fully self contained and works offline.

## Privacy

Nothing you type ever leaves your machine. There is no network request, no analytics, and no storage. All hashing and verification happen locally in the page. This is a learning tool, but the cryptography itself is real and standards-correct.

## License

MIT. Copyright 0xelitesystem 2026.
