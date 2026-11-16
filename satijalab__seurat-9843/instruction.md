# Issue

**Title:** Drop flaky test from test_sketching.R

## Description

The test in question is failing on the [macOS builder](https://mac.r-project.org/macbuilder/submit.html) with the following errors:

```
  ══ Failed tests ════════════════════════════════════════════════════════════════
  ── Failure ('test_sketching.R:117:3'): SketchData works with SCT inputs ────────
  as.numeric(result$leverage.score[42]) not equal to 0.7583021.
  1/1 mismatches
  [1] 0.755 - 0.758 == -0.00317
  ── Failure ('test_sketching.R:122:3'): SketchData works with SCT inputs ────────
  colnames(result[["sketch"]])[42] not equal to "TTTAGCTGTACTCT".
  1/1 mismatches
  x[1]: "ACGTGATGCCATGA"
  y[1]: "TTTAGCTGTACTCT"
  
  [ FAIL 2 | WARN 1528 | SKIP 26 | PASS 756 ]
  Error: Test failure
``` 

Since I'm out of time, I'm just going to drop the test and re-introduce it after the 5.3.0 release 🤷

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `875a82c83982`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.