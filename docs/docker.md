# Pearl mining with Docker

Docker is optional. Native miner packages are usually simpler for permanent rigs, while containers are convenient for quick tests and reproducible deployments.

## Requirements

You need:

- a supported GPU driver installed on the host;
- Docker;
- NVIDIA Container Toolkit for NVIDIA containers;
- GPU access inside Docker.

Check NVIDIA GPU access:

```bash
docker run --rm --gpus all nvidia/cuda:12.4.1-base-ubuntu22.04 nvidia-smi
```

If the GPU is not visible here, fix the Docker runtime before starting a miner.

## PeakMiner

Official image: <https://hub.docker.com/r/peakminer/peakminer>

```bash
docker run --rm --gpus all peakminer/peakminer:latest \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u WALLET_ADDRESS/WORKER_NAME
```

Kryptex username example:

```bash
docker run --rm --gpus all peakminer/peakminer:latest \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u yourusername/WORKER_NAME
```

For production, replace `latest` with a version you have tested and that exists on Docker Hub.

## ForgeMiner

Official releases: <https://github.com/0xHashRaptor/ForgeMiner/releases>

```bash
docker run --rm --gpus all hashraptor/forge \
  --algorithm pearlhash \
  --pool prl.kryptex.network:7048 \
  --wallet WALLET_ADDRESS \
  --worker WORKER_NAME \
  --proto stratum
```

## AlphaMiner

Official releases: <https://github.com/AlphaMine-Tech/alpha-miner/releases>

AlphaMiner is designed for AlphaPool:

```bash
docker run --rm --gpus all \
  -e PEARL_ADDRESS=WALLET_ADDRESS \
  -e PEARL_WORKER=WORKER_NAME \
  -e PEARL_POOL_HOST=eu1.alphapool.tech \
  -e PEARL_POOL_PORT=5566 \
  alphaminetech/pearl-miner:latest
```

## Run in the background

Add a container name and detached mode:

```bash
docker run -d --restart unless-stopped --name pearl-miner --gpus all \
  peakminer/peakminer:latest \
  --coin pearl \
  -o prl.kryptex.network:7048 \
  -u WALLET_ADDRESS/WORKER_NAME
```

View logs:

```bash
docker logs -f pearl-miner
```

Stop and remove the container:

```bash
docker stop pearl-miner
docker rm pearl-miner
```

## Common problems

### `could not select device driver "" with capabilities: [[gpu]]`

NVIDIA Container Toolkit is missing or not configured. Verify GPU access with the CUDA test command above.

### Miner starts but does not see a GPU

Check:

- the GPU driver works on the host;
- Docker has GPU access;
- the image supports the GPU architecture;
- the host driver satisfies the image CUDA requirements;
- `--gpus all` is present.

### Pool connection error

Test the endpoint from the host:

```bash
nc -vz prl.kryptex.network 7048
```

If `nc` is missing:

```bash
sudo apt update && sudo apt install -y netcat-openbsd
```

Check whether the selected miner expects TCP port `7048` or SSL/TLS port `8048`.

## Security notes

- Use only official images and release pages.
- Pin a tested image version in production.
- Do not expose miner APIs publicly without authentication and firewall rules.
- Review environment variables and command history before inserting sensitive pool credentials.
