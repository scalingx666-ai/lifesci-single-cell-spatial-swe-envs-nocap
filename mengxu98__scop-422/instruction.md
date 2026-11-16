# Issue

**Title:** fix: build scTenifoldKnk network ensembles natively

## Description

## Problem

`RunscTenifoldKnk(backend = "cpp")` selected its network-construction implementation from `store_networks`: the default `TRUE` routed the ensemble to `scTenifoldNet::makeNetworks()`, whose per-gene full economy SVD is quadratic in the gene count, while `store_networks = FALSE` used scop's native kernel. Reported in #418 as hours instead of minutes on identical parameters.

`store_networks` only decides whether the WT/KO tensors are kept in `srt@tools`, so it no longer changes the computation. The `cpp` backend is fully native now and no longer requires `scTenifoldNet`; the stage message reflects that, and the documented `backend` text no longer claims `r` calls `scTenifoldKnk::scTenifoldKnk()`.

## Validation

- New `tests/testthat/test-sctenifold-knk.R`: the `cpp` backend must not call `scTenifoldNet::makeNetworks()` (fails on the previous code, pointing at the old branch), and `store_networks` only changes what is stored — same-seed `diffRegulation` is identical and `tensorNetworks` is `NULL` only when asked.
- The routing guard stubs the manifold-alignment and differential-regulation steps that need the optional `RSpectra`/`RhpcBLASctl`/`MASS` packages, so it also runs where the check installs hard dependencies only; the end-to-end storage test skips when those packages are absent.
- `test-high-memory-sparse-paths.R` and `test-cpp-backend-safety.R` pass.
- `pancreas_sub` (1001 features x 200 cells, 3 networks): 23.0 s with `store_networks = TRUE` vs 23.7 s with `FALSE`, identical `diffRegulation`, `Pdx1` ranks first.
- Same data and seed, native vs upstream ensemble: 6.2 s vs 12.4 s at 301 genes and 23.3 s vs 85.1 s at 1001 genes; the resulting networks agree to 3.4e-13.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c486c263621f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.