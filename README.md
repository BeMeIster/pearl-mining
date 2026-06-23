# Pearl Mining Notes

Simple notes for starting Pearl / PRL mining on GPU.

I made this mostly as a quick reference because Pearl mining info is scattered across pool pages, miner releases, Discord messages and random configs.

This is not an official guide. Just a practical starting point.

---

## Quick info

- Coin: Pearl / PRL
- Hardware: GPU
- Typical login format: `wallet.worker` or `username.worker`
- Example pool endpoint: `prl.kryptex.network:7048`
- Miners to check: SRBMiner, PeakMiner, WildRig

The examples below use one public Pearl pool endpoint. The same idea should work with other Pearl pools too, just replace the pool host, port and login format.

Docker notes are separate: [`docs/docker.md`](docs/docker.md)

---

## What you need

You need:

- NVIDIA GPU
- Recent NVIDIA driver
- Linux or Windows
- A PRL wallet or a pool account username
- A miner that supports Pearl / PRL

Check that your GPU is visible:

```bash
nvidia-smi
```

If `nvidia-smi` does not show your GPU, the miner will probably not work either.

---

## Login examples

PRL wallet payout:

```text
prl1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.rig1
```

Pool account / username payout:

```text
yourusername.rig1
```

Worker name can be almost anything simple:

```text
rig1
rtx4090
homepc
hive001
```

---

## Option 1: SRBMiner

Download SRBMiner-Multi from GitHub releases:

```text
https://github.com/doktor83/SRBMiner-Multi/releases
```

Unpack it, go to the miner folder and create a start file:

```bash
nano start-pearl.sh
```

Paste this:

```bash
#!/bin/bash

POOL="prl.kryptex.network:7048"
LOGIN="CHANGE_ME.rig1"

./SRBMiner-MULTI \
  --algorithm pearl \
  --pool $POOL \
  --wallet $LOGIN \
  --password x \
  --disable-cpu
```

Make it executable:

```bash
chmod +x start-pearl.sh
```

Run it:

```bash
./start-pearl.sh
```

Replace `CHANGE_ME.rig1` with your real wallet or username.

---

## Option 2: PeakMiner

PeakMiner can run directly, without Docker.

Download PeakMiner from releases:

```text
https://github.com/peakminer/peakminer/releases
```

Unpack it, go to the miner folder and make the binary executable:

```bash
chmod +x peakminer
```

Run it:

```bash
./peakminer \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u CHANGE_ME.rig1
```

Example:

```bash
./peakminer \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u prl1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.rig1
```

If the binary has a different name in your release archive, use that file name instead.

---

## Option 3: WildRig

WildRig may support Pearl depending on the version.

Download WildRig from releases:

```text
https://github.com/andru-kun/wildrig-multi/releases
```

Use the same general settings:

```text
Pool: prl.kryptex.network:7048
Login: wallet.worker
Password: x
```

Check the miner help output for the exact algorithm name and options:

```bash
./wildrig-multi --help
```

---

## Docker

Docker is useful if you do not want to install the miner directly on the host.

I moved Docker examples here:

```text
docs/docker.md
```

---

## Pool example

Example endpoint used in this note:

```text
prl.kryptex.network:7048
```

Example page with more configs:

```text
https://pool.kryptex.com/prl
```

You can use another Pearl pool if you prefer. Replace the endpoint and login format with whatever that pool requires.

---

## Common problems

### Miner does not start

Check:

- driver is installed
- GPU is visible in `nvidia-smi`
- miner build matches your OS
- miner version supports Pearl / PRL
- your GPU is supported by the miner

---

### Cannot connect to pool

Check:

- pool host and port are correct
- firewall is not blocking the connection
- VPS / provider / country is not blocking stratum traffic
- try another network if possible

Example test:

```bash
nc -vz prl.kryptex.network 7048
```

If `nc` is not installed:

```bash
sudo apt update && sudo apt install -y netcat-openbsd
```

---

### Invalid wallet or login

Use one of these formats:

```text
PRL_WALLET.worker
```

or:

```text
USERNAME.worker
```

Examples:

```text
prl1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.rig1
johnminer.rig1
```

Do not put spaces in the login.

---

### Very low hashrate

Check:

- power limit
- overclock settings
- miner version
- driver version
- GPU temperature
- if another process is using the GPU

Run:

```bash
nvidia-smi
```

---

## Windows / HiveOS / other setups

This note is mostly for quick manual setup.

For Windows, HiveOS and ready-made examples, check pool pages and miner release notes.

Useful links:

```text
https://pool.kryptex.com/prl
https://github.com/doktor83/SRBMiner-Multi/releases
https://github.com/peakminer/peakminer/releases
https://github.com/andru-kun/wildrig-multi/releases
```

---

## FAQ

### How do I mine Pearl / PRL?

Use a Pearl-compatible GPU miner and connect it to a Pearl pool.

Basic format:

```text
miner + pool endpoint + wallet.worker
```

---

### Can I mine Pearl on GPU?

Yes, Pearl / PRL is mined on GPU.

---

### Which miner should I use?

Check SRBMiner, PeakMiner and WildRig first. Miner support changes often, so release notes are usually the best source.

---

### Can I use another pool?

Yes. Replace the pool endpoint and login format with the settings from your pool.

---

## Notes to add later

- HiveOS example
- Windows batch file
- simple proxy setup
- fastest stratum check
- more troubleshooting examples
- screenshots
