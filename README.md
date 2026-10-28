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
echo '<the SIGNER line of https://noisestorage.com/install.sh>' > allowed_signers
ssh-keygen -Y verify -f allowed_signers -I noisestorage-release -n noisestorage-release -s SHA256SUMS.sig < SHA256SUMS
sha256sum -c SHA256SUMS
sudo bash setup.sh
```
