# Issue

**Title:** feat: add moscot real-time CellRank backend

## Description

Add experimental-time fate analysis through `RunCellRank(kernel_type = "moscot")`. The Python backend solves adjacent time-point transport problems and passes them to CellRank's RealTimeKernel, with separate OT and within-time transition settings.

Changes include numeric time-label mapping, temporal provenance in the existing CellRank result, earliest-time random walks and flow plots, and a Python dependency profile verified in a Windows smoke run. The existing WOT and other kernel entry points remain available.

The CI follow-up makes the Cell2fate runner cache test independent of the installed thisutils Python logger, while preserving exception behavior and all cache/locking assertions. It also resolves the flow plot's `probability` global-binding NOTE.

### Validation

- Python syntax validation and `pkgload::load_all(".", quiet = TRUE, compile = FALSE)` passed.
- The formerly failing Cell2fate cache/locking subprocess test passed locally with a real Python interpreter and a test-local logger.
- The moscot (18 assertions) and CellRank/Palantir closure (36 assertions) test files passed; existing Seurat matrix-conversion warnings remain. Static usage checking no longer reports the flow `probability` binding.
- The requested local `--no-manual --as-cran --no-examples --no-tests` check was attempted. Compilation/linking completed, but installation stopped while staging R dependencies: `cannot link from D:/R-4.5.2/library/cli` to a temporary RLIBS directory on C:. The local full check is therefore not passed. The complete Cell2fate test file also has local executable-discovery failures outside the repaired subprocess case; the repaired case itself ran and passed.
- A previous Windows smoke run solved two 30 x 30 OT problems and completed the 90-cell RealTimeKernel/GPCCA/fate/plot path. Its temporary environment, script, plots and RDS were removed at the user's request.
- That smoke run does not establish numerical parity with every upstream plotting/estimator operation or Linux/macOS runtime support. The new CI run determines cross-platform R package-check status.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4286f756d4e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.