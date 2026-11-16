# Issue

**Title:** feat(tl): optional min_mean gene filter for tl.infercnv

## Description

Summary: This PR adds `min_mean` to `tl.infercnv`, an optional filter of lowly expressed genes like R inferCNV's `cutoff`. It is off by default, so results don't change unless it is set.

Changes:
- `tl.infercnv(min_mean=None)`:
  - Genes whose mean normalised expression across all cells is below `min_mean` are left out before the windows are formed.
  - The mean is computed on `expm1` of the log-normalised input, i.e. on normalised counts.
  - R inferCNV applies its cutoff to raw counts and suggests 0.1 for 10x and 1 for Smart-seq2. The two scales match when the data is normalised to the median total count, which is scanpy's default. The docstring says this.
- The means come from two new parallel numba kernels for CSR and dense blocks, so in-memory, backed and dask input all work.
- The number of removed genes is logged, and `min_mean` is recorded in `uns[key_added]["params"]`. If no genes are left, it raises an error.

Testing:
- A run with the filter gives the same result as a run on the kept genes alone (bitwise for CSR and dense, close for lazy input).
- `min_mean=None` and `0` match the default bitwise.
- The full suite passes on the cluster (459 passed, 12 skipped), and so do prek and mypy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `705ddd5f942d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.