# btcrouternode.sigs

Signed statements from the people who built or checked each
[btcrouternode](https://github.com/btcrouternode/btcrouternode) release — the
same idea as Bitcoin Core's [guix.sigs](https://github.com/bitcoin-core/guix.sigs).
Trust does not rest on one key or one person: compare the hashes of the files
you downloaded with what the builders you trust have signed here.

```
<version>/<builder>/SHA256SUMS       hashes of the release files
<version>/<builder>/SHA256SUMS.asc   the builder's PGP signature of SHA256SUMS
builder-keys/<builder>.asc           the builders' PGP public keys
```

## Checking a release

```bash
gpg --import builder-keys/*.asc
gpg --verify 24.10.8.29.3.118/eugene/SHA256SUMS.asc 24.10.8.29.3.118/eugene/SHA256SUMS
# in the folder with your downloaded files:
sha256sum --ignore-missing -c /path/to/btcrouternode.sigs/24.10.8.29.3.118/eugene/SHA256SUMS
```

Check each builder's key fingerprint against `MAINTAINERS.md` / `SECURITY.md` in
the main repository **and** on [btcrouternode.org](https://btcrouternode.org),
which is published separately from GitHub.

| Builder | PGP fingerprint |
|---------|-----------------|
| eugene | `5271 52B5 9BFA 6688 43A4  30A6 06D0 406C 5CF2 4C42` |

## What a signature here means (today)

A builder's signature says: *I built these files from the signed release tag
`v<version>` of btcrouternode, and these are their SHA256 hashes.* For the
`…-squashfs-sysupgrade.itb` image — the one routers install through Settings —
it also means the image carries the firmware signature of a maintainer's
firmware key (Release 1: Eugene's `2e51b93dd6058ffb`, itself signed by his PGP
key in the main repository).

Builds are **not yet reproducible**, so for now the hashes can only be signed by
the maintainer who made the release. Once they are (phase 2 of
[RELEASE_PROCESS.md](https://github.com/btcrouternode/btcrouternode/blob/main/docs/RELEASE_PROCESS.md)),
anyone who builds the same tag gets the same hashes and can add their own
signed folder here.

## Adding your attestation

Fork, add `<version>/<your name>/SHA256SUMS` and `SHA256SUMS.asc`
(`gpg --armor --detach-sign SHA256SUMS`) and, the first time,
`builder-keys/<your name>.asc`; open a pull request. Commits need a
`Signed-off-by` line (`git commit -s`), as in the main repository.
