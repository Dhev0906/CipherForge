# CipherForge

**A secure OpenPGP-based digital trust platform.**

CipherForge lets you generate OpenPGP key pairs, encrypt and sign messages, and decrypt and verify them — entirely in the browser, with no server, backend, or account required. It's built to make the four pillars of secure communication tangible: **confidentiality**, **integrity**, **authentication**, and **non-repudiation**.

## Why

Sensitive information is shared across platforms constantly, but most everyday messaging has no way to guarantee a message wasn't read in transit, altered, or sent by someone impersonating the sender. CipherForge applies OpenPGP encryption and digital signatures — the same standard behind PGP/GPG — to demonstrate how these guarantees actually work, end to end.

| Threat | How CipherForge addresses it |
|---|---|
| Unauthorized access | End-to-end encryption — only the recipient's private key can decrypt |
| Data tampering | Digital signatures detect any modification to a signed message |
| Identity spoofing | Signature verification confirms a message's actual sender |
| Repudiation | A valid signature can't be denied by the sender after the fact |

## Features

- **Forge Keys** — generate an OpenPGP key pair (ECC / Curve25519) from a name, email, and passphrase
- **Seal & Sign** — encrypt a message to a recipient's public key, optionally signing it with your own private key
- **Open & Verify** — decrypt a message with your private key and passphrase, and verify the sender's signature against tampering or spoofing
- **Vault** — a session-scoped keyring holding your own identities (private + public key) and contacts (public key only)
- Clear pass/fail states for wrong passphrases, mismatched keys, and failed signature checks — no silent failures

## How it works

CipherForge runs entirely client-side using [OpenPGP.js](https://openpgp.js.org/), loaded from a CDN at runtime (with automatic fallback across cdnjs, jsdelivr, and unpkg if one is unreachable). All keys, messages, and vault contents live only in the browser tab's memory for that session — nothing is persisted to disk or sent to a server. Reloading the page clears everything.

This makes it suitable as a demo or teaching tool, but **not** as a production key manager — see [Security notes](#security-notes) below.

## Getting started

CipherForge is a single self-contained HTML file. No build step, no dependencies to install.

1. Download `CipherForge.html`
2. Open it in any modern browser (Chrome, Firefox, Edge, Safari)
3. An internet connection is required on first load, to fetch the OpenPGP.js library

To serve it locally instead of opening the file directly:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/CipherForge.html
```

## Usage

1. **Forge a key pair** for yourself under *Forge Keys* — this becomes an identity in your vault
2. **Add a contact** under *Vault* by pasting their public key (or forge a second identity to test with)
3. **Seal & sign** a message to that contact, optionally signing as yourself
4. **Open & verify** the sealed message using the recipient's identity, checking the sender's signature

## Tech stack

- Vanilla HTML/CSS/JavaScript — no framework or build tooling
- [OpenPGP.js v5](https://github.com/openpgpjs/openpgpjs) for all cryptographic operations (key generation, encryption, signing, decryption, verification)

## Security notes

- This project is a **mini-project / learning demonstration**, not an audited security product
- Keys are held in memory only for the current browser tab and are never written to disk, cookies, or `localStorage`
- Closing or reloading the tab permanently discards any generated keys — export and store them safely if you want to keep them
- OpenPGP.js itself has undergone independent security audits, but this application's UI and key-handling code have not

## Roadmap ideas

- Offline bundling of OpenPGP.js so no CDN/internet dependency is needed after first load
- Import/export of the vault as an encrypted file
- Support for RSA key generation alongside ECC
- Detached signatures for signing files rather than just text

## Team

- J. Dhevshri
- Govarthini S

## License

Add a license of your choice (e.g. MIT) before publishing.

