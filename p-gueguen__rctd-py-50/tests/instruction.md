# Issue

**Title:** Fix GPU out-of-memory with batch_size="auto" in doublet and multi mode

## Description

`batch_size="auto"` (the Python API default) sized every mode's batches from full mode's memory per pixel. In doublet mode a batch row is a (pixel, type, type) triple and in multi mode a candidate type set, each with its own (G, k) design matrix, and the dense (N, G) counts these modes keep on the GPU were not subtracted. On a 44 GB L40S, doublet and multi mode on 39k Visium HD segmented cells (4,747 genes, 40 types, float64) got 200,000-row batches and ran out of memory. Found while answering #49. `rctd run` (default `--batch-size 10000`) was not affected.

**Changes**
- `auto_batch_size` takes `mode`, `n_resident`, `max_multi_types` and `device`. The cost per batch row is set per mode above peaks measured with `torch.cuda.max_memory_allocated` (L40S, G 1,500-25,000, K 10-150, float32 and float64): full 7.5-14 x G, doublet 20-21.5 x G, multi up to 18.4 x G. Measured / estimated is 0.44-0.76 in every case. Doublet and multi take the larger of their own row and the full-mode fit they start with.
- Memory that does not grow with the batch is subtracted from free memory: the resident counts (except in full mode with `stream_gpu=True`) and the G x K² `P_outer` table of the full-mode fit. Free memory is read from `config.device`; on CPU the default is returned.
- An unknown `mode` raises; G or K <= 0 returns the default. A warning says when the counts, or the 1,024-row minimum batch, do not fit.
- `tests/test_auto_batch_size.py`: unit tests, plus a `slow` GPU test that runs each mode at two batch sizes and fails if the measured peak per row exceeds the estimate (cases up to G=18,000 and K=40 in float64). With the old estimate it fails in all three modes.

**Trade-offs**
The row costs are measured constants rather than derived from tensor shapes; the GPU test is what catches drift when the solver changes. Batches are smaller than before in every mode, so `"auto"` weights can differ from 0.4.3 in the last digits (noted in the changelog). On the run below, auto batches were no faster than `batch_size=10000`.

**Verification** (L40S, issue #49 data, 38,990 cells)

| mode | main, auto | this PR, auto | peak | vs `batch_size=10000` |
|---|---|---|---|---|
| full, float64 | ok (batch covers all cells) | ok | 13.5 GiB | `converged` identical, weights ≤ 4e-14 |
| doublet, float64 | out of memory | ok | 25.4 GiB | labels identical, weights ≤ 4e-14 |
| multi, float64 | out of memory | ok | 15.4 GiB | labels identical, weights ≤ 7e-14 |
| doublet, float32 | - | ok | 20.6 GiB | labels identical, weights ≤ 4e-4 |

Synthetic data, auto batch filling the budget, 14 configurations up to G=25,000 and K=150: no out-of-memory, peaks 8-48% of free memory. Full test suite on the GPU node: 245 passed. Not measured on Blackwell cards.

🤖 Prepared with assistance from Claude Opus 5.5 via Claude Code.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66f31e7c1d67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.