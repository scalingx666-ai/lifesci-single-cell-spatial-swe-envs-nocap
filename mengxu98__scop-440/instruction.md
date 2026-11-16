# Issue

**Title:** fix(geneset): follow GSVA 2.6 sparse scoring and support CRAN RcppML

## Description

## What

- The native Gaussian GSVA kernel now reproduces the sparse running-sum walk of the installed GSVA release: GSVA <= 2.4 places a gene set's zero-expression genes by global gene index, GSVA >= 2.6 spreads them across the zero-rank block in gene-set order. Both placements are implemented and selected by the detected version.
- The walk is evaluated only at the gene-set hit positions, removing the per-set `O(n_genes)` pass.
- Explicitly stored zeros are dropped before scoring, so `backend = "cpp"` and `backend = "r"` agree regardless of how the sparse matrix was built.
- `RunNMF()` works with the CRAN `RcppML` release: the `Matrix` attach required by RcppML <= 0.3.7.1 is scoped to the call, and `check_r()` no longer replaces an installed CRAN build with the GitHub one.
- New `suggests-contract` job in `R-CMD-check` runs the gene-set scoring contracts on pull requests instead of only in the weekly coverage job.

## Verification (local, R 4.5.3)

- native vs delegated, GSVA 2.6.6 and 2.4.9: `max|diff| = 0` for ascending, shuffled, duplicated and overlapping gene sets, `tau = 0.5`, `abs_ranking`, `max_diff = FALSE`, and inputs with explicitly stored zeros.
- Legacy path vs the pre-change build: `identical()` on 7 configurations.
- `RunGSVA()` / `CellScoring()` cpp vs r end to end: `max|diff| = 0` (0.59 / 0.55 before, on stored-zero input).
- Timing, GSVA 2.6.6, 2,000 x 1,000 sparse / 400 gene sets: native 33 ms vs delegated 1,695 ms (~51x); 1,500 x 300 / 400 sets: 21 ms vs 58 ms for the previous walk (~2.8x).
- Targeted sweep: 66 blocks / 228 assertions, 0 failures, with GSVA 2.4.9 and 2.6.6 and the CRAN RcppML build.

`R CMD check` and the new contract job run on this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b020110b45b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.