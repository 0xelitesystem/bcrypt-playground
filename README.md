# bcrypt playground

An educational, fully client-side bcrypt playground. Generate and verify bcrypt hashes, inspect the anatomy of a hash string, and learn why bcrypt is the right tool for password storage. Everything runs in your browser with no external dependencies.

**Live demo:** https://0xelitesystem.github.io/bcrypt-playground/

## Use

1. Type a password, set the Cost factor (4 to 15) and pick `$2a$` or `$2b$`.
2. Click Generate hash and read the hash anatomy: prefix, cost, salt and digest.
3. To check a password, paste a bcrypt hash and the password to test, then click Verify for MATCH or NO MATCH.

## Why this exists

bcrypt is easier to trust once you have taken a hash apart. This page implements bcrypt from scratch so you can generate, verify and dissect hashes without sending a password to a server. It is one HTML file with no tracking, MIT licensed.

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

## Run locally

```
git clone https://github.com/0xelitesystem/bcrypt-playground
cd bcrypt-playground
```

Open `index.html` in any modern browser, or serve the folder with `python -m http.server 8000` and visit http://localhost:8000/.

## Build

No build step. The whole tool is one `index.html` file with inline CSS and JavaScript.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright RBL Industries LLC 2026.
