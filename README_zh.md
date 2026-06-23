# pearl-mining

[English](README.md) | **中文**

一些关于 Pearl / PRL GPU 挖矿的小笔记。

主要是命令、链接，还有一些不想每次重新找的东西。

---

## 快速开始

1. 准备 PRL 钱包，或者矿池账号用户名。
2. 选择矿工：SRBMiner、PeakMiner、WildRig。
3. 登录格式用 `wallet.worker` 或 `username.worker`。
4. 如果用别的矿池，替换下面的 pool 地址即可。

下面用到的示例地址：

```text
prl.kryptex.network:7048
```

基本格式：

```text
miner + pool endpoint + wallet.worker
```

---

## 登录格式

直接挖到 PRL 钱包：

```text
prl1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.rig1
```

挖到矿池账号 / 用户名：

```text
yourusername.rig1
```

worker 示例：

```text
rig1
rtx4090
homepc
hive001
```

---

## SRBMiner

Release 页面：

```text
https://github.com/doktor83/SRBMiner-Multi/releases
```

示例 `start-pearl.sh`：

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

运行：

```bash
chmod +x start-pearl.sh
./start-pearl.sh
```

---

## PeakMiner

Release 页面：

```text
https://github.com/peakminer/peakminer/releases
```

示例：

```bash
chmod +x peakminer

./peakminer \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u CHANGE_ME.rig1
```

如果压缩包里的二进制文件名不一样，就用实际文件名。

---

## WildRig

Release 页面：

```text
https://github.com/andru-kun/wildrig-multi/releases
```

基本配置：

```text
Pool: prl.kryptex.network:7048
Login: wallet.worker
Password: x
```

具体算法名和参数看当前版本：

```bash
./wildrig-multi --help
```

---

## Docker

Docker 不是必须的。单独放这里，README 会短一点：

[docs/docker.md](docs/docker.md)

---

## 备注

- Pearl / PRL 是 GPU 挖矿。
- 启动矿工前，`nvidia-smi` 应该能看到显卡。
- 如果连不上矿池，检查 host、port、防火墙，以及网络/服务商是否拦截 stratum。
- 矿工支持更新很快，所以 release notes 通常比旧配置更有用。
- 其他矿池大体类似，但登录格式和协议细节可能不同。

常用链接：

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
