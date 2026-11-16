# Issue

**Title:** release: 0.4.1 (lower GPU memory, same results)

## Description

Release 0.4.1: lower GPU memory, same results as 0.4.0.

- #42 (Bowen-Man): sigma tables staged one pair at a time, bulk reductions on the CPU, IRWLS temporaries reused, `stream_gpu` for full mode.
- Float64 GPU eigh in chunks of 1,024 for matrices up to 32 x 32: multi mode peaks at 945 MiB instead of 5,378 MiB on Xenium and 9.4 instead of 12.1 GB on Visium HD. Float32 keeps one call (chunking moved float32 weights by up to 4e-4).
- `rctd run --stream-gpu` (full mode only).
- Docs: CHANGELOG 0.4.1, GPU memory section corrected (streaming: 6.9 -> 4.0 GB at batch 10000, ~1.1 GB at batch 1024), quickstart and benchmark notes, docstrings, repo agent docs.

Bit-identical to the released 0.4.0 at the same `batch_size`: every comparison on Xenium (all modes, float32/float64, 12-type reference) and Visium HD (doublet, multi, full with streaming), plus the CLI, on an L40S and on CPU. GPU test suite: 194 + 17 slow passed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b8f4af4c58a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.