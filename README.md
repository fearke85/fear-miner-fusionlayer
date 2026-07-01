# FearMiner (FusionLayer / FXL)

GPU miner for **FusionLayer (FXL)** — FusionHash (cn/gpu) algorithm.

> This repository hosts **release binaries only**. The source code is not
> published here yet. Grab the latest build from the
> [**Releases**](../../releases) page.

## Downloads

Each release ships builds for both GPU vendors and both platforms:

| Platform | OpenCL (AMD + NVIDIA) | CUDA (NVIDIA only) |
|---|---|---|
| **Windows x64** | `fear-miner.exe` | `fear-miner-cuda.exe` + `fusionhash_cuda.dll` + `cudart64_12.dll` |
| **Linux / HiveOS** | `fear-miner` | `fear-miner-cuda` |

- **AMD GPUs:** use the OpenCL build (`fear-miner` / `fear-miner.exe`).
- **NVIDIA GPUs:** prefer the **CUDA** build — it is faster and more accurate on
  share correctness. The OpenCL build also runs on NVIDIA as a fallback.
- The CUDA build requires its DLLs (`fusionhash_cuda.dll`, `cudart64_12.dll`) to
  sit in the **same folder** as the executable.

## Quick start

List detected GPUs:

```bat
fear-miner.exe -info -all
fear-miner-cuda.exe -info
```

Local performance test (no pool):

```bat
fear-miner.exe -mock -all
```

Mine to a pool:

```bat
fear-miner.exe      -pool=wss://HOST:PORT -user=WALLET.WORKER -pass=x
fear-miner-cuda.exe -pool=wss://HOST:PORT -user=WALLET.WORKER -pass=x
```

## Common flags

| Flag | Description |
|---|---|
| `-pool` | Pool endpoint (FusionLayer stratum-over-websocket, e.g. `wss://host:port`) |
| `-user` | `wallet.worker` |
| `-pass` | Pool password (usually `x`) |
| `-devices` / `-d` | 1-based device indices (comma-separated); empty = all |
| `-all` | Include non-AMD/NVIDIA devices (Intel, etc.) |
| `-intensity` | Intensity multiplier (lower it on out-of-memory errors) |
| `-worksize` | Override work size (8, 16, 32; 0 = auto) |
| `-tui` | Terminal UI (logs redirect to `logs/`) |
| `-info` | List devices and exit |
| `-mock` | Local benchmark, no pool |

## Verifying downloads

Every release includes a `SHA256SUMS.txt`. Check your download before running:

```bat
certutil -hashfile fear-miner-cuda.exe SHA256
```

```bash
sha256sum -c SHA256SUMS.txt
```

## Support

Open an [issue](../../issues) for bugs or questions.
