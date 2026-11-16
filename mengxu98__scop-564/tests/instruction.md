# Issue

**Title:** perf: remove dense-matrix blowups and loop write amplification

## Description

## Summary

Output-equivalent performance fixes: 15 files, +116 / -51. No public API, algorithm semantics or numeric changes.

### Loop write amplification

| File | Change |
| --- | --- |
| `R/CallATACPeaks.R` | `on.exit()` writes commands/receipt once instead of twice per MACS2 process |
| `R/DataConvert.R` | list collection + one `unlist()` instead of `c()` accumulation |
| `R/PrepareDB.R` | merge manifest rows once; compute md5/file size once per file |
| `R/RunSpatialIntegration.R` | `do.call(c/rbind, ...)` once |
| `R/PrepareCCCDB.R` | drop unconditional `Sys.sleep(0.5)` on cache hit |

### Sparse matrices & distances

- `R/RunCellRank.R`: `Matrix::colSums(x > 0)` on sparse input; subset columns before densifying
- `R/RunGNIPLR.R`: only dense-convert non-matrix inputs
- `R/RunPHATE.R`, `R/RunIntegration.R`: row-wise `vapply` instead of the `apply(d, 1, order)` n x n integer matrix; fallback reads `stats::dist()`'s packed vector directly

### Python / polling / C++

- `inst/python/spatialdm_runner.py`: one `(X > 0).sum(axis=0)` pass
- `inst/python/functions.py`: numpy pre-filter for GNIPLR candidates
- `R/RunSpatialBenchmark.R`: 20 Hz wait with 600 s timeout
- `src/Manifold.cpp`, `src/GNIPLR.cpp`: `reserve()` with known upper bounds

## Behaviour change

`commands.rds` / `receipt.rds` are now written once on exit (including on error) instead of after each process. Failure diagnostics are preserved and `man/CallATACPeaks.Rd` is updated. A hard SIGKILL no longer leaves intermediate state.

Also fixes `graph_conn_edges_r()` returning `1 x n` instead of `n x 1` when `k = 1`.

## Validation

| Check | Result |
| --- | --- |
| Syntax | 284 R files parse; `py_compile`; `g++ -fsyntax-only` |
| Build/tests | `pkgload::load_all()` + 59 testthat cases, 0 failed / 0 error / 0 skipped |
| Equivalence | triplets/sparse matrix, dist row reconstruction, top-k indices, GNIPLR candidates, sparse column counts (incl. duplicate gene names), `on.exit` success/failure paths |
| Benchmark (n = 4000) | intermediate scratch 61 MB -> 0.2 MB; runtime ~unchanged |

## Notes

Algorithm-level changes with numeric drift are out of scope (PHATE C++ kNN, `SpatialGradient.cpp` KD-tree, sparse GNIPLR interface); `RunGENIE3.R`'s `as.matrix()` is required by GENIE3. Security findings from the review are tracked separately.

Supersedes #563 after renaming the head branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dba12251a532`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.