# pearl-mining

**English** | [中文](README_zh.md)

Small notes for mining Pearl / PRL on GPUs.

Mostly commands, links, and things I do not want to search for twice.

---

## Quickstart

1. Get a PRL wallet or a pool account username.
2. Pick a miner for your GPU:
   - NVIDIA: SRBMiner, PeakMiner, WildRig
   - AMD: krig-miner
3. Use the login format expected by the miner and pool.
4. Replace the example pool if you use another one.

Example endpoints used below:

```text
prl.kryptex.network:7048
prl.kryptex.network:8048
```

These are just example endpoints. You can use another Pearl pool if the miner supports its protocol.

Basic shape:

```text
miner + pool endpoint + wallet/worker login
```

---

## Login

A common direct wallet login looks like:

```text
prl1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.rig1
```

Pool account / username payout:

```text
yourusername.rig1
```

Some miners use a different worker separator. For example, `krig-miner` uses:

```text
WALLET/WORKER
```

Worker examples:

```text
rig1
rtx4090
rx7900xt
homepc
hive001
```

---

## NVIDIA GPUs

### SRBMiner

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

### PeakMiner

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

### WildRig

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

## AMD GPUs

### krig-miner

`krig-miner` is a Pearl GPU miner with a ROCm backend for AMD cards.

Repository and releases:

```text
https://github.com/kryptex/krig-miner
https://github.com/kryptex/krig-miner/releases
```

Pick the build matching your ROCm setup, then make the binary executable. If the downloaded file has a versioned name, rename it first:

```bash
mv krig-miner-* krig-miner
chmod +x krig-miner
```

Check that ROCm can see the GPU:

```bash
rocminfo
```

Start mining:

```bash
./krig-miner \
  --url prl.kryptex.network:8048 \
  --user CHANGE_ME/rig1
```

Same command with short options:

```bash
./krig-miner \
  -o prl.kryptex.network:8048 \
  -u CHANGE_ME/rig1
```

Optional password:

```bash
./krig-miner \
  -o prl.kryptex.network:8048 \
  -u CHANGE_ME/rig1 \
  -p x
```

Useful checks:

```bash
./krig-miner --help
./krig-miner --version
```

The upstream repository currently lists tested examples across RDNA 2, RDNA 3, and RDNA 4 cards. Actual hashrate depends on the GPU, ROCm version, clocks, power limits, and the rest of the system.

---

## Docker

Docker is optional. I keep it separate to avoid bloating this page:

[docs/docker.md](docs/docker.md)

---

## Notes

- Pearl / PRL mining is GPU mining.
- On NVIDIA, `nvidia-smi` should see the GPU before starting the miner.
- On AMD, check the ROCm stack first; `rocminfo` should see the GPU.
- If the pool does not connect, check host, port, firewall, and provider/network blocks.
- Miner support changes fast, so release notes are usually more useful than old configs.
- Other pools should work in the same general way, but login format and protocol quirks can differ.
- Do not blindly copy worker separators between miners: `wallet.worker` and `wallet/worker` are not always interchangeable.

Useful links:

```text
https://github.com/doktor83/SRBMiner-Multi/releases
https://github.com/peakminer/peakminer/releases
https://github.com/andru-kun/wildrig-multi/releases
https://github.com/kryptex/krig-miner/releases
```

---

## TODO

- Windows batch file
- HiveOS config
- tested configs
- simple proxy notes
- fastest stratum check
