# Pearl 挖矿

[English](README.md) | **中文**

Pearl（PRL）当前公开 GPU 矿工及可直接修改的配置示例。

> 最后检查：**2026-07-27**。这里只收录有公开下载页面和可验证启动参数的矿工。完整说明、区域节点、Docker 和故障排查请查看 [English README](README.md)。

## Kryptex 矿池

```text
TCP:     prl.kryptex.network:7048
SSL/TLS: prl.kryptex.network:8048
```

登录格式因矿工而异：

```text
WALLET_ADDRESS.WORKER_NAME
WALLET_ADDRESS/WORKER_NAME
WALLET_ADDRESS --worker WORKER_NAME
```

Kryptex 用户名通常可以替代 PRL 钱包地址。SOLO 模式在支持的矿工中使用 `solo:` 前缀。

## 当前矿工

| 矿工 | 显卡 | 系统 |
|---|---|---|
| SRBMiner-MULTI | AMD、NVIDIA | Windows、Linux、HiveOS |
| WildRig Multi | AMD、NVIDIA | Windows、Linux、HiveOS |
| BzMiner | AMD、NVIDIA、Intel | Windows、Linux、HiveOS |
| PeakMiner | NVIDIA、AMD | Windows、Linux、HiveOS、Docker |
| ForgeMiner | NVIDIA | Windows、Linux、HiveOS、Docker |
| ARCMiner | Intel Arc | Windows |
| lpminer | NVIDIA | Windows、Linux、HiveOS |
| Krig miner | AMD；NVIDIA 测试版 | Windows、Linux |
| RGMiner | NVIDIA | Windows、Linux、HiveOS、MMPOS |
| HydraX | NVIDIA | Windows、Linux、HiveOS |
| NPMiner | NVIDIA | Windows、Linux、HiveOS、MMPOS |
| AlphaMiner | NVIDIA | Linux、HiveOS、Docker |

## SRBMiner-MULTI

下载：<https://github.com/doktor83/SRBMiner-Multi/releases>

```bash
./SRBMiner-MULTI --disable-cpu --algorithm pearlhash --pool prl.kryptex.network:7048 --wallet WALLET_ADDRESS.WORKER_NAME --password x
```

SSL/TLS：

```bash
./SRBMiner-MULTI --disable-cpu --algorithm pearlhash --pool prl.kryptex.network:8048 --wallet WALLET_ADDRESS.WORKER_NAME --password x --tls true
```

## WildRig Multi

下载：<https://github.com/andru-kun/wildrig-multi/releases>

```bash
./wildrig-multi --algo pearlhash --url prl.kryptex.network:7048 --user WALLET_ADDRESS.WORKER_NAME --pass x
```

## BzMiner

下载：<https://github.com/bzminer/bzminer/releases>

```bash
./bzminer -a pearl -p stratum+tcp://prl.kryptex.network:7048 -w WALLET_ADDRESS/WORKER_NAME --nvidia 1 --amd 1 --intel 1 --igpu 0 --cpu 0 --cpu_threads 0 --nc 1
```

## PeakMiner

下载：<https://github.com/peakminer/peakminer/releases>

```bash
./peakminer --coin pearl -o prl.kryptex.network:7048 -u WALLET_ADDRESS/WORKER_NAME
```

## ForgeMiner

下载：<https://github.com/0xHashRaptor/ForgeMiner/releases>

```bash
./forge --algorithm pearlhash --pool prl.kryptex.network:7048 --wallet WALLET_ADDRESS --worker WORKER_NAME --proto stratum
```

## ARCMiner

下载：<https://github.com/jbman2025/ARC-miner/releases/tag/ARC-Miner-Release>

Intel Arc、Windows 实验版本：

```bat
arc-miner.exe --pool stratum+tcp://prl.kryptex.network:7048 --wallet WALLET_ADDRESS --worker WORKER_NAME
```

## lpminer

下载：<https://github.com/BaikalMine-Pools/pearl-miner/releases>

```bash
./lpminer --algo pearl --pool stratum+tcp://prl.kryptex.network:7048 --wallet WALLET_ADDRESS.WORKER_NAME
```

## Krig miner

下载：<https://github.com/kryptex/krig-miner/releases>

Krig 主要针对 AMD 优化，NVIDIA 支持仍为测试版。当前使用 SSL/TLS 端口：

```bash
./krig-miner --url prl.kryptex.network:8048 --user WALLET_ADDRESS/WORKER_NAME
```

## RGMiner

下载：<https://github.com/Printscan/rgminer/releases>

```bash
./rgminer --algo pearl --stratum prl.kryptex.network:7048 --wallet WALLET_ADDRESS --worker-name WORKER_NAME --proto kryptex
```

## HydraX

下载：<https://hydrax.gg/>

```bash
./miner -a pearlhash -o prl.kryptex.network:7048 -u WALLET_ADDRESS.WORKER_NAME
```

## NPMiner

下载：<https://nushypool.com/downloads>

Pearl 支持为实验功能。NushyPool 示例：

```bash
./npminer -a pearl -o stratum+tcp://nushypool.com:40015 -u WALLET_ADDRESS -w WORKER_NAME
```

## AlphaMiner

下载：<https://github.com/AlphaMine-Tech/alpha-miner/releases>

AlphaMiner 是 AlphaPool 专用矿工：

```bash
./alpha-miner --pool stratum+tcp://eu1.alphapool.tech:5566 --address WALLET_ADDRESS --worker WORKER_NAME
```

## Docker

PeakMiner、ForgeMiner 和 AlphaMiner 的 Docker 命令：

[docs/docker.md](docs/docker.md)

## 注意

- 算法名可能是 `pearl` 或 `pearlhash`，必须按矿工要求填写。
- worker 分隔符可能是 `.`、`/`，也可能需要单独参数。
- TCP 端口为 `7048`，SSL/TLS 端口为 `8048`。
- 只从开发者官方页面下载。
- 新版本先在独立矿机测试，再部署到全部设备。
- `cnminer`、`tw-pearl-miner`、`pcm`、`pearl-native` 等没有可靠公开下载和配置页面的构建暂不收录。
