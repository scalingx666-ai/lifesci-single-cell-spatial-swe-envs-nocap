# Issue

**Title:** fix: keep scTenifoldKnk network scores when re-embedding subsamples

## Description

.

`RunscTenifoldKnk(backend = "cpp")` re-embeds each subsampled network into the full gene space by assigning the coefficients into an empty matrix. That matrix was built with `Matrix::sparseMatrix(i = integer(0), j = integer(0), dims = ...)` and no `x =` argument, which returns a *pattern* (`ngCMatrix`) matrix. Assigning doubles into it coerced them to logical — the `val is coerced to logical for "ngCMatrix" x` warnings — and left the network without weights and with a single surviving entry.

The branch is entered whenever a subsample drops an all-zero gene, so it fires in essentially every network on real data with a detection tail. The tensor decomposition then received logical matrices, which `Rcpp` silently coerced back to 0/1, so the run completed with warnings only and the knocked-out gene lost its edges and its significance.

It became the default in 0.9.1, when the `cpp` backend stopped routing through `scTenifoldNet::makeNetworks()` (#422); before that only `store_networks = FALSE` reached this path.

The empty matrix now carries `x = numeric(0)`, matching the numeric matrix that `scTenifoldNet::makeNetworks()` builds before coercion to `dgCMatrix`. The ensemble then agrees with the upstream construction to floating-point round-off (~1e-14), and manifold alignment and differential regulation were already numerically identical between the two backends.

### Tests

`tests/testthat/test-sctenifold-knk.R` gains a fixture whose gene has no counts in any cell, so every subsample exercises the re-embedding branch:

- one test asserts the networks keep numeric weights (dgCMatrix, non-trivial nnzero and value spread, no warning) on both the dual and the primal solver;
- a second compares the ensemble element-wise against `scTenifoldNet::makeNetworks()` where that package is installed.

Both fail on the pre-fix code (14 and 4 failures) and pass with it. `test-sctenifold-knk.R` and `test-high-memory-sparse-paths.R` pass, run the way CI runs them (`test_local(filter =, load_package = "source")`).

Note the `optional-backends.yaml` matrix has no scTenifoldNet suite, so the parity test skips in CI; the invariant test runs everywhere.

### Real-data validation

`pancreas_sub`, 501 genes including 200 sitting at the detection boundary, `nc_nNet = 3`, `nc_nCells = 150`:

| | before | after | `backend = "r"` |
|---|---|---|---|
| `replCmat4` warnings | 3 | 0 | 0 |
| `Pdx1` rank | 148 | 1 | 1 |
| `Pdx1` p.adj | 0.957 | 0 | 0 |

`panc8_sub`, 3246 features (2821 genes after QC), `nc_nNet = 10`, `nc_nCells = 150`, `cores = 4`:

| | before | after |
|---|---|---|
| `replCmat4` warnings | 10 | 0 |
| `PDX1` rank | 2378 | 1 |
| `PDX1` Z / p.adj | -0.96 / 0.9993 | 19.08 / 0 |
| tensor network nnzero | 4 | 7,351,703 |

Both before-columns reproduce the numbers reported in #427.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f0dab03615be`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.