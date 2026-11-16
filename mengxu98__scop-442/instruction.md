# Issue

**Title:** fix: preserve scCODA automatic reference selection

## Description

## Summary

`RunscCODA()` currently converts `NULL` to an empty string, and the Python
wrapper silently replaces any empty or unknown reference-cell value with the
first cell type. This means the official scCODA `reference_cell_type="automatic"`
selection is never used through SCOP, and an invalid explicit cell type can
silently change the analysis reference.

This patch:

- defaults the R and Python wrappers to `"automatic"`;
- passes the value through to scCODA unchanged;
- normalizes legacy `NULL`/empty values to `"automatic"`;
- validates explicit cell-type names and raises an actionable error instead of
  silently selecting the first column;
- documents and tests the behavior.

The official scCODA implementation then performs its own automatic reference
selection based on prevalence and relative-abundance dispersion.

## Tests

```text
/hwdata/home/jinqc/miniconda3/envs/scop/bin/Rscript -e 'pkgload::load_all(".", quiet=TRUE, compile=FALSE); testthat::test_file("tests/testthat/test-sccoda.R", reporter="summary", stop_on_failure=TRUE)'
```

Result: `sccoda: ...........` and `DONE`.

Also verified `inst/python/functions.py` with Python AST parsing and
`git diff --check`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee77fd106c33`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.