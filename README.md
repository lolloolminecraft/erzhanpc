# Erzhan PC — signed updates

This public repository is an update channel for the **Erzhan PC** Windows agent. It does not contain the complete source code, private API keys, tunnel credentials, or the publisher's private signing key.

The app checks [`channel.json`](channel.json) periodically and when the user clicks **Check for updates**. Every channel announcement is authenticated with a pinned Ed25519 public key. Each update is verified using both an Ed25519 signature and the package SHA-256 before activation.

## Small updates

For a release after the 2.3.0 installer, the publisher creates a cumulative ZIP containing only changed Python modules at the archive root and/or `icons/*.svg`, signs the release manifest, uploads the ZIP under `releases/`, and replaces `channel.json` with the signed patch manifest.

The app downloads the ZIP (maximum 8 MB), checks its integrity and allowed entries, saves it locally and activates it on restart. The original bundled application remains available as a fallback if the patch cannot be validated. Updates to the bootstrap/updater itself still require a new signed installer.

**Signing is not encryption.** Package integrity and publisher identity are checked; a public ZIP can be inspected by anyone. HTTPS protects transfer. The publisher keeps the encrypted private key separately from this repository.

## Safety

Connected tools cannot change the trusted update publisher. The local user controls the update key and has to approve downloading or activating new updates. The Risk and Crazy automation modes are temporary and are not saved across restarts.

This repository does not include an Authenticode certificate. Windows Defender/SmartScreen reputation depends on trusted code signing, distribution and Microsoft's own scanning. Don't disable antivirus protection for this application.
