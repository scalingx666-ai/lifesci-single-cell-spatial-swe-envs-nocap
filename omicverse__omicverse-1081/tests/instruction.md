# Issue

**Title:** ov.vi DDP: fix Dask(cupy) crash on rank>0 + first 2×H100 verification

## Description

First real multi-GPU run of ov.vi DDP (#1074) on 2× H100.

- Verified: NCCL DDP for in-memory / AnnDataOOM / Dask; `train(devices=[0,1])` and torchrun; disjoint per-rank sharding; latent quality = 1-GPU (BMMC, SEA-AD 300k, full SEA-AD 1.38M); save/load after DDP; no HDF5 lock errors with a concurrent writer process.
- Fix: `DaskSource` crashed rank 1 with cudaErrorIllegalAddress — cupy's thread-local current device defaulted to 0 inside dask pool threads. Now computes blocks synchronously inside an explicit `cupy.cuda.Device(idx)` context. 1-GPU Dask epoch time unchanged (4.84 → 4.83 s, SEA-AD 300k; one delayed task per block).
- New GPU-skipped test `test_ddp_dask_cupy_two_gpus`; results in `benchmarks/vi/results_ddp.md`.
- Scaling note: on this shared node (GPUs ~97% busy with other jobs, 8 CPUs) 2 GPUs were slower than 1 (0.4–0.7×); needs re-measuring on idle GPUs.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc512ac5a990`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.