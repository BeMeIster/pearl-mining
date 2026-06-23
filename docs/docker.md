# Pearl Mining with Docker

Docker is optional.

Use it if you want to test mining quickly without unpacking a miner directly on the host.

For normal rigs, native miner launch is usually simpler.

---

## Requirements

You need:

- NVIDIA driver installed on the host
- Docker installed
- NVIDIA Container Toolkit installed
- GPU visible in Docker

Check GPU on the host:

```bash
nvidia-smi
```

Check GPU inside Docker:

```bash
docker run --rm --gpus all nvidia/cuda:12.4.1-base-ubuntu22.04 nvidia-smi
```

If this does not show your GPU, fix Docker GPU support first.

---

## PeakMiner Docker example

Basic command:

```bash
docker run -it --rm --gpus all peakminer/peakminer:latest \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u CHANGE_ME.rig1
```

Example with PRL wallet:

```bash
docker run -it --rm --gpus all peakminer/peakminer:latest \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u prl1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.rig1
```

Example with username:

```bash
docker run -it --rm --gpus all peakminer/peakminer:latest \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u yourusername.rig1
```

---

## Fixed miner version

Using `latest` is convenient, but it can change.

If you want repeatable behavior, pin the image version:

```bash
docker run -it --rm --gpus all peakminer/peakminer:1.0.6 \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u CHANGE_ME.rig1
```

Use the version that actually exists on Docker Hub.

---

## Common Docker problems

### `could not select device driver "" with capabilities: [[gpu]]`

NVIDIA Container Toolkit is probably missing or not configured.

Check Docker GPU support first:

```bash
docker run --rm --gpus all nvidia/cuda:12.4.1-base-ubuntu22.04 nvidia-smi
```

---

### Container starts but miner does not see GPU

Check:

- `nvidia-smi` works on the host
- Docker has GPU access
- correct image is used
- driver is new enough

---

### Pool connection error

Test connection from the host:

```bash
nc -vz prl.kryptex.network 7048
```

If `nc` is not installed:

```bash
sudo apt update && sudo apt install -y netcat-openbsd
```
