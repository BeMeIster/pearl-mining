# Pearl mining

**English** | [中文](README_zh.md)

Current public GPU miners for **Pearl (PRL)** with copy-paste configurations.

> Last reviewed: **2026-07-27**. Only publicly downloadable miners with a verifiable release page and command-line configuration are listed.

## Quick start

1. Get a PRL wallet or use your Kryptex username.
2. Pick a miner that supports your GPU and operating system.
3. Replace `WALLET_ADDRESS` and `WORKER_NAME` in the example.
4. Download miners only from the official links below.

## Kryptex pool endpoints

| Region | TCP | SSL/TLS |
|---|---|---|
| Global | `prl.kryptex.network:7048` | `prl.kryptex.network:8048` |
| Europe | `prl-eu.kryptex.network:7048` | `prl-eu.kryptex.network:8048` |
| North America | `prl-us.kryptex.network:7048` | `prl-us.kryptex.network:8048` |
| Brazil | `prl-br.kryptex.network:7048` | `prl-br.kryptex.network:8048` |
| Singapore | `prl-sg.kryptex.network:7048` | `prl-sg.kryptex.network:8048` |
| Hong Kong | `prl-hk.kryptex.network:7048` | `prl-hk.kryptex.network:8048` |
| Russia | `prl-ru.kryptex.network:7048` | `prl-ru.kryptex.network:8048` |
| UAE | `prl-ae.kryptex.network:7048` | `prl-ae.kryptex.network:8048` |

For SOLO mining, prefix the login with `solo:` where supported:

```text
solo:WALLET_ADDRESS.WORKER_NAME
```

## Login formats

Different miners use different worker separators. Do not replace one format with another unless the miner supports it.

```text
WALLET_ADDRESS.WORKER_NAME
WALLET_ADDRESS/WORKER_NAME
WALLET_ADDRESS --worker WORKER_NAME
```

A Kryptex username can usually be used instead of a PRL wallet:

```text
yourusername.WORKER_NAME
```

## Miner overview

| Miner | GPUs | Platforms | Pool support |
|---|---|---|---|
| [SRBMiner-MULTI](#srbminer-multi) | AMD, NVIDIA | Windows, Linux, HiveOS | Multiple pools |
| [WildRig Multi](#wildrig-multi) | AMD, NVIDIA | Windows, Linux, HiveOS | Multiple pools |
| [BzMiner](#bzminer) | AMD, NVIDIA, Intel | Windows, Linux, HiveOS | Multiple pools |
| [PeakMiner](#peakminer) | NVIDIA, AMD | Windows, Linux, HiveOS, Docker | Multiple pools |
| [ForgeMiner](#forgeminer) | NVIDIA | Windows, Linux, HiveOS, Docker | Multiple pools |
| [ARCMiner](#arcminer) | Intel Arc | Windows | Multiple pools |
| [lpminer](#lpminer) | NVIDIA | Windows, Linux, HiveOS | Multiple pools |
| [Krig miner](#krig-miner) | AMD; NVIDIA beta | Windows, Linux | Kryptex |
| [RGMiner](#rgminer) | NVIDIA | Windows, Linux, HiveOS, MMPOS | Multiple pools |
| [HydraX](#hydrax) | NVIDIA | Windows, Linux, HiveOS | Multiple pools |
| [NPMiner](#npminer) | NVIDIA | Windows, Linux, HiveOS, MMPOS | Experimental Pearl support |
| [AlphaMiner](#alphaminer) | NVIDIA | Linux, HiveOS, Docker | AlphaPool-specific |

---

## SRBMiner-MULTI

Official downloads: <https://github.com/doktor83/SRBMiner-Multi/releases>

Pearl algorithm name: `pearlhash`.

### Linux

```bash
./SRBMiner-MULTI \
  --disable-cpu \
  --algorithm pearlhash \
  --pool prl.kryptex.network:7048 \
  --wallet WALLET_ADDRESS.WORKER_NAME \
  --password x
```

### Windows

```bat
SRBMiner-MULTI.exe --disable-cpu --algorithm pearlhash --pool prl.kryptex.network:7048 --wallet WALLET_ADDRESS.WORKER_NAME --password x
```

### SSL/TLS

```bash
./SRBMiner-MULTI --disable-cpu --algorithm pearlhash --pool prl.kryptex.network:8048 --wallet WALLET_ADDRESS.WORKER_NAME --password x --tls true
```

---

## WildRig Multi

Official downloads: <https://github.com/andru-kun/wildrig-multi/releases>

```bash
./wildrig-multi \
  --algo pearlhash \
  --url prl.kryptex.network:7048 \
  --user WALLET_ADDRESS.WORKER_NAME \
  --pass x
```

Windows uses the same arguments with `wildrig.exe` or the executable name included in the release archive.

Optional Pearl kernel settings vary between releases. Check them before use:

```bash
./wildrig-multi --help
```

---

## BzMiner

Official downloads: <https://github.com/bzminer/bzminer/releases>

```bash
./bzminer \
  -a pearl \
  -p stratum+tcp://prl.kryptex.network:7048 \
  -w WALLET_ADDRESS/WORKER_NAME \
  --nvidia 1 \
  --amd 1 \
  --intel 1 \
  --igpu 0 \
  --cpu 0 \
  --cpu_threads 0 \
  --nc 1
```

Windows uses the same arguments with `bzminer.exe`.

Recent beta builds may expose Pearl optimization modes such as `--pearl_opt auto`, `eff`, `hr`, or `lowmem`. Confirm availability with the release notes or `--help` before adding them.

---

## PeakMiner

Official downloads: <https://github.com/peakminer/peakminer/releases>

```bash
./peakminer \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u WALLET_ADDRESS/WORKER_NAME
```

Windows:

```bat
peakminer.exe --coin pearl -o prl.kryptex.network:7048 -u WALLET_ADDRESS/WORKER_NAME
```

Docker and HiveOS examples are available in [docs/docker.md](docs/docker.md) and the official PeakMiner README.

---

## ForgeMiner

Official downloads: <https://github.com/0xHashRaptor/ForgeMiner/releases>

```bash
./forge \
  --algorithm pearlhash \
  --pool prl.kryptex.network:7048 \
  --wallet WALLET_ADDRESS \
  --worker WORKER_NAME \
  --proto stratum
```

Windows uses the same arguments with `forge.exe`.

HiveOS custom miner package:

```text
https://github.com/0xHashRaptor/ForgeMiner/releases/latest/download/ForgeMiner.tar.gz
```

---

## ARCMiner

Official downloads: <https://github.com/jbman2025/ARC-miner/releases/tag/ARC-Miner-Release>

ARCMiner is an experimental Windows miner for Intel Arc GPUs. Select the release build matching your GPU revision.

```bat
arc-miner.exe --pool stratum+tcp://prl.kryptex.network:7048 --wallet WALLET_ADDRESS --worker WORKER_NAME
```

---

## lpminer

Official downloads: <https://github.com/BaikalMine-Pools/pearl-miner/releases>

```bash
./lpminer \
  --algo pearl \
  --pool stratum+tcp://prl.kryptex.network:7048 \
  --wallet WALLET_ADDRESS.WORKER_NAME
```

Windows uses the same arguments with `lpminer.exe`.

---

## Krig miner

Official downloads: <https://github.com/kryptex/krig-miner/releases>

Krig is optimized for AMD GPUs. NVIDIA support is beta. The miner currently uses the SSL/TLS endpoint.

```bash
./krig-miner \
  --url prl.kryptex.network:8048 \
  --user WALLET_ADDRESS/WORKER_NAME
```

Useful checks:

```bash
./krig-miner --list-devices
./krig-miner --version
./krig-miner --help
```

---

## RGMiner

Official downloads: <https://github.com/Printscan/rgminer/releases>

```bash
./rgminer \
  --algo pearl \
  --stratum prl.kryptex.network:7048 \
  --wallet WALLET_ADDRESS \
  --worker-name WORKER_NAME \
  --proto kryptex
```

RGMiner also supports pool-specific Pearl protocols. Use the matching `--proto` value when switching pools.

HiveOS custom miner package:

```text
https://github.com/Printscan/rgminer/releases/download/v1.0.0/rgminer-1.0.0.tar.gz
```

---

## HydraX

Official downloads: <https://hydrax.gg/>

```bash
./miner \
  -a pearlhash \
  -o prl.kryptex.network:7048 \
  -u WALLET_ADDRESS.WORKER_NAME
```

Windows uses the same arguments with the executable included in the release archive.

---

## NPMiner

Official downloads: <https://nushypool.com/downloads>

Pearl support is experimental and currently targets NVIDIA CUDA GPUs. NPMiner has different fee rules for NushyPool and other compatible pools.

NushyPool example:

```bash
./npminer \
  -a pearl \
  -o stratum+tcp://nushypool.com:40015 \
  -u WALLET_ADDRESS \
  -w WORKER_NAME
```

Check the current release notes before using NPMiner with another Pearl pool.

---

## AlphaMiner

Official downloads: <https://github.com/AlphaMine-Tech/alpha-miner/releases>

AlphaMiner is designed for AlphaPool and is listed separately because its connection format is pool-specific.

```bash
./alpha-miner \
  --pool stratum+tcp://eu1.alphapool.tech:5566 \
  --address WALLET_ADDRESS \
  --worker WORKER_NAME
```

Docker:

```bash
docker run --rm --gpus all \
  -e PEARL_ADDRESS=WALLET_ADDRESS \
  -e PEARL_WORKER=WORKER_NAME \
  -e PEARL_POOL_HOST=eu1.alphapool.tech \
  -e PEARL_POOL_PORT=5566 \
  alphaminetech/pearl-miner:latest
```

---

## Docker

Ready-to-use Docker examples for PeakMiner, ForgeMiner, and AlphaMiner:

[docs/docker.md](docs/docker.md)

## HiveOS

For a custom miner installation, use the archive or install URL published by the miner developer. Typical flight-sheet fields are:

```text
Pool: prl.kryptex.network:7048
Wallet template: WALLET_ADDRESS.WORKER_NAME
Algorithm: pearl or pearlhash, depending on the miner
```

Do not assume every miner uses the same algorithm name or worker separator.

## Troubleshooting

### Pool connection timeout

```bash
nc -vz prl.kryptex.network 7048
```

Check the selected region, port, firewall, hosting-provider filters, and whether the miner expects a TCP or SSL/TLS endpoint.

### Miner does not see the GPU

NVIDIA:

```bash
nvidia-smi
```

AMD with ROCm:

```bash
rocminfo
```

Intel:

```bash
sycl-ls
```

### Shares are rejected

Check:

- algorithm name: `pearl`, `pearlhash`, or a miner-specific alias;
- worker separator: `.`, `/`, or a separate `--worker` argument;
- pool protocol option, if the miner exposes one;
- TCP versus SSL/TLS port;
- whether SOLO requires a `solo:` login prefix.

## Not listed yet

Private, pool-internal, unavailable, or insufficiently documented builds are not presented as downloadable miners. This currently includes names seen in network statistics such as `cnminer`, `tw-pearl-miner`, `pcm`, `pearl-native`, and builds without a current public release/configuration page.

A miner can be added through a pull request when it has:

1. an official public download or release page;
2. supported GPU and OS information;
3. a working Pearl command;
4. clear fee information;
5. a maintainer or support contact.

## Safety

- Download only from official developer pages.
- Verify checksums or signatures when the developer publishes them.
- Test new binaries on an isolated rig first.
- Review miner fees and pool-specific restrictions before deployment.
- Pin a tested version in production instead of silently following `latest`.
