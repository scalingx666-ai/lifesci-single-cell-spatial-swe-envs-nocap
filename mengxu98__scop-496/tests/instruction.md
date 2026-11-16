# Issue

**Title:** fix: require Rcpp 1.0.13 for CellRank compilation

## Description

CellRank builds fail with older Rcpp headers because its 25-field `List::create()` call exceeds the generated overload limit of 20 arguments. Require Rcpp >= 1.0.13 in both Imports and LinkingTo so dependency resolution upgrades incompatible installations before compilation.

Validation:
- R dependency parsing recognizes both minimum-version requirements.
- A local C++17 compilation probe with the same 25 field names fails with Rcpp 1.0.12 and passes with Rcpp 1.0.13.
- `git diff --check` passes.

The customer Windows installation has not been rerun.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `53ed7e08f354`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.