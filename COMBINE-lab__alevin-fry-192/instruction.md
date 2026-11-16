# Issue

**Title:** feat(generate-permit-list): scale multi-sample barcode correction by a memory budget, not a hard cap of 4

## Description

## What this changes
Multi-sample (multiplexed Flex) `generate-permit-list` corrects cell barcodes per sample. It capped concurrent correction workers at `gpl_opts.threads.min(4).min(num_samples)` — a hard cap of **4**. This replaces the `4` with a memory-budgeted cap.

## How it helps
The hard cap of 4 serializes high-plex runs: with *N* samples, correction runs in `ceil(N/4)` round-robin rounds — a 16-sample run corrects in **4 rounds instead of 1**.

Per-sample scopes are independent once priors are frozen, and the large per-sample histograms are **partitioned** across workers (not duplicated) — only ~tens of MB of correction *scratch* scales with worker count. So concurrency is capped by a small **memory budget** (4 GiB / 128 MiB ≈ 32 scopes), bounded by `num_samples` and the caller's thread budget, rather than the arbitrary `4`.

**Measured (16-sample dataset, `-t 32`):**
- Barcode correction: **3.86 s → ~1.3 s (~3×)**; total `generate-permit-list` ~7% faster.
- **Output byte-identical**: `correction_plan.bin` sha256 unchanged; identical per-sample and total cell counts (verified across cap=4 / cap=16 / memory-budget builds).
- Peak RSS during correction rises ~0.69 GB (16 scopes × ~58 MB scratch vs 4), which stays well under the mapping-stage high-water mark → **pipeline peak RSS unchanged**.

## Scope / safety
Only affects runs with **>4 samples**; 1–4-plex behavior is identical. The memory budget bounds worst-case concurrent scratch for any plexity.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `86dd6957aeb0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.