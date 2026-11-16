# Issue

**Title:** fix: align deprecated srt alias presence handling

## Description

## Summary

The audit against `upstream/main` (`1d7d9fb7`) found no public function whose literal `srt` input still lacks the unified `object` formal:

- 347 NAMESPACE exports; 170 have both `object` and deprecated `srt`. Of those, 165 call `resolve_deprecated_srt()` directly and five native spatial APIs use `spatial_resolve_object()`, which delegates to that resolver.
- 86 registered S3 methods; none declares `srt`. `RunDEtest()` resolves its alias before dispatch; its Seurat and SummarizedExperiment methods take `object`.
- `RunVECTOR()`, `VECTORPlot()`, `RuntAge()`, `tAgePlot()`, `RunscTenifoldNet()`, and `PrepareSCExplorer()` remain object-only.
- The internal `resolve_deprecated_srt()` helper and spatial input validation helper remain in place. Multi-object interfaces and conversion/storage names are unchanged.

This PR fixes an argument-presence gap in `RunDEtest()` and the five spatial APIs. They now distinguish an omitted `object` from an explicitly supplied `object = NULL`. Supplying a non-NULL `srt` alongside an explicitly supplied `object` follows the shared resolver's duplicate-input error behavior. Positional calls and public formals are unchanged.

The deprecated `srt=` alias remains supported with a warning until scop 1.0.0, where removal is scheduled. `RunDEtest()` examples now show `object=`, with the generated Rd updated.

## Validation

- `Rscript -e 'pkgload::load_all(".", quiet=TRUE, compile=FALSE)'` passed.
- Focused tests passed: `test-spatial-object-alias.R`, `test-rundetest-findmarkers.R`, `test-cellrank-moscot.R`, and `test-spatial-input-contracts.R`.
- Rd checks and parsing of the generated `RunDEtest()` examples passed; inspected live formals for the migrated APIs, object-only exceptions, and `RunDEtest` S3 methods.
- The requested `_R_CHECK_FORCE_SUGGESTS_=false` `rcmdcheck` command and a persistent-log `R CMD check` attempt both stopped during package installation because `cc1plus.exe` ran out of memory compiling the existing `src/CellRank.cpp`. The `rcmdcheck` wrapper also hit an embedded-NUL `iconv()` error while reading the failed install log. The check did not reach dependency or examples-warning checks. A separate `test-spatial-core.R` attempt with `compile=FALSE` stopped in an unrelated CytoSPACE test because `_scop_cytospace_estimate_fractions_cpp` was unavailable.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `633c0cabc8e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.