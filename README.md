# File Integrity Checker

A lightweight, offline-first tool for hashing files and detecting changes over time. Everything runs in the browser — no install, no server, no accounts. Saved records are encrypted locally, so only you can read them.

Built by Roadlesstrodden.

## Why this exists

If you need to confirm a file hasn't been tampered with or corrupted since you last checked it, you need two things: a way to hash it, and a safe place to keep that hash for comparison later. This app does both in one place, without sending anything over the network.

## Features

- **Drag-and-drop hashing** — drop a file in and get a SHA-256 hash instantly (SHA-1 and SHA-512 also supported).
- **Automatic comparison** — if you've already saved a baseline for that filename, the app tells you immediately whether the new hash matches.
- **Encrypted local vault** — saved hashes are protected with a password. Records are encrypted with AES-256-GCM, using a key derived via PBKDF2 (250,000 iterations), before they're written to storage.
- **Tamper-evident storage** — AES-GCM includes an authentication check. If the encrypted data is altered directly (bypassing the password), it fails to decrypt rather than silently returning a forged value.
- **Portable encrypted backups** — export the vault as a `.json` file to back it up or move it to another machine. The exported file is encrypted the same way as local storage; it's useless without the password.
- **No network calls** — hashing, encryption, and storage all happen client-side. Nothing is uploaded anywhere.

## Getting started

### Run it locally
1. Download `file-hash-checker.html`.
2. Open it directly in any modern browser (Chrome, Edge, Firefox, Safari).

### Run it on GitHub Pages
1. Fork or clone this repo.
2. Rename `file-hash-checker.html` to `index.html` (or leave as-is and use the full path in the URL).
3. In **Settings → Pages**, set the source to your main branch.
4. Visit the generated `https://yourusername.github.io/repo-name/` URL.

GitHub Pages just serves the static file — no backend is involved, and hashing/encryption still all happen in your browser.

## How to use it

1. **First run:** set a vault password. This password encrypts everything you save — it is never stored anywhere, so there's no way to recover a forgotten one.
2. **Hash a file:** drag it into the drop zone, or click to browse. The hash appears immediately.
3. **Save a baseline:** click "Save as baseline" to store the hash, encrypted, for future comparison.
4. **Check later:** drop the same file in again — the app automatically compares it against the saved baseline and flags a match or mismatch.
5. **Lock the vault** when you're done, especially on a shared machine.
6. **Back up your vault** via "Export encrypted backup" and store the file somewhere separate from the machine you're protecting (USB drive, separate cloud account). This matters most if you're worried about someone tampering with both the file *and* its local record.

## Security notes

- Your vault password is never stored or transmitted — only a key derived from it (via PBKDF2) is used, and only in memory while unlocked.
- Storage is scoped per-browser and per-URL. Clearing site data, switching browsers, or moving to a new machine means starting over unless you've exported a backup.
- Encryption protects the *stored data* from casual tampering or inspection — it does not protect against someone who already knows your password, or against malware with full access to an unlocked session.
- Avoid MD5 or SHA-1 for anything security-sensitive; they're included for compatibility, but SHA-256 or SHA-512 are recommended for integrity checks that matter.

## License

MIT — see LICENSE. Reuse and modification are welcome; the license asks that the "Built by Roadlesstrodden" attribution stay intact in any copy or derivative.
