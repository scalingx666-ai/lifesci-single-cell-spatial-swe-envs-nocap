# Issue

**Title:** Skip unused Monocle2 dispersion fitting on the R backend

## Description

## Summary
- `RunMonocle2(backend = "r")` now skips `estimateDispersions()` unless `feature_type = "Disp"` or `show_plot = TRUE`, matching the C++ backend.
- Default HVF trajectory runs no longer densify the full count matrix.
- Large-matrix overflow in dispersion fitting is fixed in [mengxu98/monocle](https://github.com/mengxu98/monocle) 2.9.3; install that release for `feature_type = "Disp"`.

## Test plan
- [x] `monocle2_needs_dispersion()` unit checks for HVF vs Disp vs `show_plot`
- [ ] After installing monocle 2.9.3, `RunMonocle2(srt, group.by = ..., backend = "r")` on a large object completes
- [ ] Existing R vs C++ backend ordering tests still pass

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3cd75cd509a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.