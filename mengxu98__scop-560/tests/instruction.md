# Issue

**Title:** fix: forward RunMonocle2 verbosity to dimensionality reduction

## Description

RunMonocle2() defaults to verbose = TRUE, but omitted that argument when calling Monocle's reduceDimension(), whose default is FALSE. Forward verbose through the existing argument builder so the default run emits DDRTree progress and verbose = FALSE remains quiet.

Add a real-backend regression test comparing default and quiet runs, checking progress output and identical reductions, states, and pseudotime. Update NEWS without changing dependencies or public defaults.

Validation:
- Monocle2 test file: 20 assertions passed with monocle 2.9.3 and DDRTree 0.1.6 on Windows / R 4.5.2.
- pkgload::load_all(..., compile = FALSE) completed, with a native DLL-loading warning in this uncompiled worktree.
- styler checked both changed R files; no formatting changes needed. git diff --check passed.
- Required R CMD check --no-manual --as-cran --no-examples --no-tests started with _R_CHECK_FORCE_SUGGESTS_=false; currently pending at CRAN incoming feasibility. Dependency-code and example-dependency checks are not yet verified.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f5a66cc370c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.