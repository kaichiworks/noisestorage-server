# NoiseStorage server releases

Encryption First, Owner Only.

Signed releases of the NoiseStorage server, the storage end of an end-to-end encrypted personal storage: it keeps
only encrypted chunks and never sees file contents, names or keys. The source is not in this repository.

Each release has the server for Linux (`e2e-server-x86_64`, `e2e-server-aarch64`), `setup.sh`, `SHA256SUMS` and its
signature `SHA256SUMS.sig`, and the same files as one `.tar.gz`.

## Install

On an Ubuntu 24.04 VPS:

```bash
curl -fsSL https://noisestorage.com/install.sh | sudo bash
```

`install.sh` downloads the latest release from here, checks the signature and the SHA-256 of each file, and runs
`setup.sh`, which asks a few questions. Run the same line again to update; the data stays.

## Checking a release by hand

```bash
tar xzf noisto-server-<version>.tar.gz && cd noisto-server-<version>
echo 'noisestorage-release namespaces="noisestorage-release" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICpmkWdxhIwaLjfd8YJKrqj+M7neEG7WRSLbMZYi84ZI' > allowed_signers
ssh-keygen -Y verify -f allowed_signers -I noisestorage-release -n noisestorage-release -s SHA256SUMS.sig < SHA256SUMS
sha256sum -c SHA256SUMS
sudo bash setup.sh
```

The release signing key (Ed25519, fingerprint `SHA256:prSH83/BHAfWZHgmUCawObaWBHNpNyy+sUkursYv6nM`) is the same as the `SIGNER` line of
https://noisestorage.com/install.sh.
