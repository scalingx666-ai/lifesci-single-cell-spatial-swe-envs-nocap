# Issue

**Title:** fix: accept default empty moscot arguments in RunCellRank

## Description

## Summary

`RunCellRank(kernel_type = "moscot")` failed before OT when callers left `moscot_args` and `realtime_args` at their R defaults of `list()`. Reticulate converts those empty lists to Python `[]`, which the bridge rejected as a non-mapping.

Treat empty Python lists or tuples as empty mappings before validating the moscot configuration. Non-empty unnamed sequences remain invalid.

This PR contains only the default-argument fix; the moscot backend itself was merged in #438.

## Validation

- Focused `test-cellrank-moscot.R` tests pass on this branch.
- Real 80-cell, two-time-point Seurat smoke run completed moscot OT, RealTimeKernel, CellRank CFLARE and GPCCA fate probabilities, Seurat result conversion, and the flow plot with the patched bridge.
- Python syntax parsing and `git diff --check` pass.
- Local patched-SCOP `R CMD check --as-cran --no-manual --no-examples --no-tests`: 0 errors, 0 warnings, 3 notes. The required R-code and examples dependency checks were both OK.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0bd2c25c79e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.