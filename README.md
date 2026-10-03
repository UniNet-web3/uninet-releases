# UniNet node releases

Signed builds of the UniNet node for Linux x86_64 (Ubuntu 22.04 or newer, Debian 12).
The source is developed in a separate repository; this one only publishes the programs.

## Install a node on your own server

```bash
curl -fsSL https://uninet.technology/install.sh | sudo bash
```

On a cloud that keeps the public address off the server's interface (AWS, GCP, Azure),
name it:

```bash
curl -fsSL https://uninet.technology/install.sh | sudo bash -s -- --ip YOUR_PUBLIC_IP
```

Add `--auto-update` to install each new release by itself, once a day.

The node starts as an observer and syncs the chain. To validate, its wallet needs 1,000 UNE
for the stake and a little more for fees ([faucet](https://uninet.technology/faucet)), then:

```bash
sudo validator-join.sh apply && sudo validator-join.sh stake
```

and the current validators vote it in (`sudo validator-join.sh status` shows where it
stands).

## Update

```bash
sudo uninet-update
```

## What is in a release

| File | What it is |
|------|------------|
| `uninet-node-linux-x86_64.tar.gz` | `uninet-node`, `uninet-cli`, `validator-join.sh`, `uninet-update`, `VERSION` |
| `VERSION` | the release's version |
| `SHA256SUMS` | the sums of the two files above |
| `SHA256SUMS.sig` | the Ed25519 signature over `SHA256SUMS` by the UniNet release key |

The installer and the updater check the signature and the sums before they install
anything. To check by hand, with the release key from the installer:

```bash
openssl pkeyutl -verify -pubin -inkey release-key.pub -rawin -in SHA256SUMS -sigfile SHA256SUMS.sig
sha256sum -c SHA256SUMS
```
