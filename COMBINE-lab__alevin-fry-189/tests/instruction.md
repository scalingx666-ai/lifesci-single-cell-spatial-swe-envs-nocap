# Issue

**Title:** perf(quant): stream the count matrix instead of buffering it whole

## Description

## Summary

The final count-matrix write in `quantify` was the pipeline's peak-memory step.
Every nonzero was gathered into per-worker `Vec`s, concatenated into a global
`all_triplets: Vec<(usize, usize, f32)>` (24 B/nonzero), then copied a second
time into an `sprs::TriMatI` (12 B/nonzero) right before `write_matrix_market`.
Peak was therefore ~36 B/nonzero, and for multiplexed libraries the nonzero
count is the total across all samples in a single matrix.

This PR writes `quants_mat.mtx` incrementally. Each worker formats a cell's
entries into a reusable thread-local `String` and appends them to a shared
`BufWriter` under a dedicated mutex (separate from the barcode/feature lock, so
neither critical section lengthens the other) — no triplet buffer is ever
materialized. `rows`/`cols` are known up front; the size line's `nnz` is not, so
a fixed-width field is reserved and patched with `seek` after the workers join.

## Measured impact

16-plex human Flex, 2,566,288 cells × 18,129 genes, **600,187,015 nonzeros**, 32 threads:

| | before | after |
|---|--:|--:|
| Peak RSS (VmHWM) | 26.3 GB | **6.6 GB** (−75%) |
| Wall time | 603 s | 613 s (neutral) |

After the change the peak is the mapping stage, not quant.

## Correctness

Output is equivalent to a stock build — verified on the same library:

- dims (2566288×18129), nnz (600187015), total UMI (1767485205): identical
- per-gene column sums, per-cell row-sum multiset: identical
- `quants_mat_cols.txt` byte-identical; `quants_mat_rows.txt` identical barcode set; `featureDump.txt` unchanged; identical set of output files

Only the cell (row) order in the matrix differs — which is already
thread-nondeterministic between two stock runs.

## Note on the size line

The patched size line is right-padded with trailing spaces to the reserved
field width, e.g. `2566288 18129 600187015    `. MatrixMarket parsers tokenize
that line on whitespace runs, so `scipy.io.mmread`, `anndata`/`scanpy`, and R
`Matrix::readMM` all parse it identically to an unpadded line (verified on all
three); only the size line is padded — data lines are clean. If a byte-identical
size line is preferred, the body can be streamed to a temp file and a clean
header prepended, at the cost of one extra pass.

## Scope

Bootstrap summary matrices (`bootstraps_{mean,var}.mtx`) are left on the previous
accumulate-then-write path, as they are off the default (`--num-bootstraps 0`)
code path.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `afa67499c595`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.