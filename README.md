# pearl-mining

**English** | [中文](README_zh.md)

Small notes for mining Pearl / PRL on GPUs.

Mostly commands, links, and things I do not want to search for twice.

---

## Quickstart

1. Get a PRL wallet or a pool account username.
2. Pick a miner: SRBMiner, PeakMiner, WildRig.
3. Use `wallet.worker` or `username.worker` as login.
4. Replace the example pool if you use another one.

Example endpoint used below:

```text
prl.kryptex.network:7048
```

Basic shape:

```text
miner + pool endpoint + wallet.worker
```

---

## Login

Direct PRL wallet payout:

```text
prl1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.rig1
```

Pool account / username payout:

```text
yourusername.rig1
```

Worker examples:

```text
rig1
rtx4090
homepc
hive001
```

---

## SRBMiner

Releases:

```text
https://github.com/doktor83/SRBMiner-Multi/releases
```

Example `start-pearl.sh`:

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

Run:

```bash
chmod +x start-pearl.sh
./start-pearl.sh
```

---

## PeakMiner

Releases:

```text
https://github.com/peakminer/peakminer/releases
```

Example:

```bash
chmod +x peakminer

./peakminer \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u CHANGE_ME.rig1
```

If the binary has another name in the archive, use that name instead.

---

## WildRig

Releases:

```text
https://github.com/andru-kun/wildrig-multi/releases
```

Basic settings:

```text
Pool: prl.kryptex.network:7048
Login: wallet.worker
Password: x
```

Check the exact algorithm/options in your build:

```bash
./wildrig-multi --help
```

---

## Docker

Docker is optional. I keep it separate to avoid bloating this page:

[docs/docker.md](docs/docker.md)

---

## Notes

- Pearl / PRL mining is GPU mining.
- `nvidia-smi` should see the GPU before starting the miner.
- If the pool does not connect, check host, port, firewall, and provider/network blocks.
- Miner support changes fast, so release notes are usually more useful than old configs.
- Other pools should work in the same way, but login format and protocol quirks can differ.

Useful links:

```text
https://pool.kryptex.com/prl
https://github.com/doktor83/SRBMiner-Multi/releases
https://github.com/peakminer/peakminer/releases
https://github.com/andru-kun/wildrig-multi/releases
```

---

## TODO

- Windows batch file
- HiveOS config
- tested configs
- simple proxy notes
- fastest stratum check
