This repository contains Guix attestations for releases of Dpowcore Core.

## Overall process

The Guix build consists of two stages:

- In the first stage (`noncodesigned`), people compile the binaries from source.
- Then, code signatures for Windows and MacOS are generated from the binaries that were produced in the first stage, and [distributed](https://github.com/bitcoin-core/bitcoin-detached-sigs) to the builders. ( Not used we dont have codesign signature )
- In the second stage (`all`), the builders attach these code signatures.  ( Not used we dont have codesign signature )

See https://github.com/dpowcore-project/dpowcoin/blob/master/doc/release-process.md#building on how to build the release with Guix and create an attestation.

## Directory structure

- `/<version>/<signer>/`: Build attestations for repository tag `v<version>` for `<signer>`.
    - `noncodesigned.SHA256SUMS`: Hashes of binaries produced by the first stage build for this version.
    - `noncodesigned.SHA256SUMS.asc`: Detached PGP signature for `noncodesigned.SHA256SUMS`.
    - `all.SHA256SUMS`: Hashes of binaries produced by the second stage build. This covers all the binaries uploaded to the website, and is what to check release binaries against.
    - `all.SHA256SUMS.asc`: Detached PGP signature for `all.SHA256SUMS`.  ( Not used we dont have codesign signature )
- `/builder-keys/<signer>.gpg`: PGP keys of the signers. If you're going to do builds and contribute attestations, file a PR to add your key here.
- `/contrib`: Scripts used in the CI tests.
