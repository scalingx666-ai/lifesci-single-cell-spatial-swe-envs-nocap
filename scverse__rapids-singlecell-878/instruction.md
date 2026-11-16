# Issue

**Title:** Harmony: drop `shuffle_chunk_size`, pick the update-block runs internally

## Description

`shuffle_chunk_size` (#829) is removed from `pp.harmony_integrate` and `harmonize`. Cells keep joining the update blocks in runs of up to 8 neighbouring batch-sorted cells, now an internal constant that is still clamped to a block's share (`n_cells // n_blocks`). Seeded results are bitwise unchanged (checked for one and two keys, float64, bfloat16 and a 150-cell input with clamped runs).

## Why the function picks it
The cells are already in random order within each batch, and every block takes the same share of each stretch of about n/384 sorted cells. So the run length only decides how evenly a batch of fewer than ~`8 / block_proportion` (160) cells spreads over the blocks, against speed: runs keep the rows contiguous, and the assignment kernel starts a partial tile for every batch in a block, so single cells leave many near-empty tiles when there are many small batches. Nobody can judge that per dataset, and runs of 8 get most of the speed without changing results on real data.

### Quality
Five seeds per setting, default parameters. Paired change of runs of 8 / 32 against single cells: iLISI over the batches (perplexity 30), purity of the cell types among the 30 nearest neighbours, and on synthetic data the recall of the 30 true (batch-free) neighbours.

| Data | batches (< 160 cells) | iLISI | purity | true neighbours | rel. L2 to single cells | rel. L2 between seeds |
|---|---|---|---|---|---|---|
| IRcolitis CD8, 69k cells, `donor_batch` | 81 (11) | −0.03% / −0.23% | +0.01% / +0.07% | | 0.92% / 1.22% | 6.95% |
| IRcolitis CD8, `batch` | 11 | 0.00% / 0.00% | 0.00% / 0.00% | | 0.13% / 0.13% | 3.76% |
| Kang 2018, 25k cells, `replicate` | 8 | 0.00% / 0.00% | 0.00% / 0.00% | | 0.08% / 0.08% | 1.04% |
| 213k census subset, `assay` | 3 | 0.00% / 0.00% | 0.00% / 0.00% | | 0.06% / 0.06% | 4.01% |
| 213k census subset, `donor_id` | 12 | 0.00% / 0.00% | 0.00% / 0.00% | | 0.11% / 0.11% | 4.74% |
| 11.3M tiled atlas (metrics on 300k cells) | 74 (2) | 0.00% / 0.00% | 0.00% / 0.00% | | 0.35% / 0.35% | 1.78% |
| synthetic, 6 large + 300 small batches | 306 (300) | 0.00% / +0.01% | 0.00% / 0.00% | 0.00% / 0.00% | 0.03% / 0.10% | 0.17% |
| synthetic, 1500 batches of 40 | 1500 (1500) | 0.00% / 0.00% | 0.00% / 0.00% | 0.00% / 0.00% | 0.11% / 0.31% | 0.28% |
| synthetic, overlapping types, 6 large + 300 small | 306 (300) | −0.50% / −1.77% | +0.24% / +0.59% | +0.86% / +2.69% | 1.83% / 2.82% | 5.42% |
| synthetic, overlapping types, 800 batches of 10–150 | 800 (800) | +0.05% / +0.05% | +0.40% / +1.74% | +2.37% / +9.88% | 8.03% / 12.10% | 29.45% |

On real data, runs of 8 change no metric by more than 0.03% (runs of 32 by at most 0.23%), and the outputs differ from single cells by a fraction of the seed-to-seed difference. Only hundreds of tiny batches with overlapping cell types (synthetic) shift, the same way for every seed: runs of 8 lower iLISI by up to 0.5% and recover 0.9–2.4% more of the true neighbours, runs of 32 about three times as much. Likely because a block holding a run of a tiny batch holds out more of that batch's counts: a mild discount of tiny batches, in the direction of `tau`.

### Speed
NVIDIA GB10, full `harmonize` call with a fixed 10 × 4 iterations, median of 5 interleaved runs (3 for the atlas):

| Data | cells × PCs | batches | single cells | runs of 2 | 4 | 8 | 16 | 64 |
|---|---|---|---|---|---|---|---|---|
| 213k census subset | 213k × 100 | 3 | 249 ms | −0.7% | −1.3% | **−1.4%** | −1.5% | −1.4% |
| IRcolitis CD8 | 69k × 50 | 81 | 80 ms | −0.3% | −1.4% | **−1.6%** | −1.5% | −1.2% |
| synthetic | 60k × 30 | 1500 | 220 ms | −4.9% | −10.5% | **−15.4%** | −19.2% | −22.1% |
| synthetic | 1.0M × 200 | 122 | 2,047 ms | −0.8% | −1.0% | **−1.3%** | −1.3% | −2.0% |
| synthetic | 2.0M × 50 | 100 | 1,015 ms | −2.4% | −3.7% | **−4.2%** | −4.7% | −5.2% |
| synthetic | 4.0M × 20 | 50 | 1,398 ms | −4.6% | −6.6% | **−7.6%** | −7.8% | −8.3% |
| tiled atlas | 11.3M × 50 | 74 | 4,911 ms | −3.9% | −5.6% | **−6.4%** | −6.7% | −7.6% |

## Changes
- `pp.harmony_integrate`, `harmonize`: no `shuffle_chunk_size`; `_SHUFFLE_CHUNK = 8` in `_harmony`. The `block_proportion` docs say how the runs spread small batches.
- Tests: the parameter's validation cases are gone; `test_harmony_block_runs` checks the clamp and that runs of one are reproducible and differ from runs of 8.
- Release note: the `shuffle_chunk_size` line is removed.

`tests/test_harmony.py` and `tests/test_harmony_kernels.py` on one GB10: 360 passed, 39 skipped.

Data: IRcolitis CD8 blood cells (the Harmony test data, 50 PCs, 8 clusters); Kang 2018; the 213k-cell CELLxGENE census subset of the notebooks (100 PCs, 16 cell types); Gaussian cell types with batch-specific shifts, the unshifted cells as ground truth; and the 213k set tiled 53 times with jitter and 74 skewed batches as a stand-in for the 11.4M-cell atlas of #829, which is not on this machine.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5c546fcd3f5e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.