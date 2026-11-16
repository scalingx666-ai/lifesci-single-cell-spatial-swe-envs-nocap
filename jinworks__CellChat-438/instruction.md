# Issue

**Title:** Fix: Enable parallelization in computeCommunProb bootstrap loop

## Description

## Problem
`computeCommunProb` runs single-threaded even when `future::plan()` is configured with multiple workers. This was reported in #411 but closed without a fix.

## Root Cause
Line 261 in `R/modeling.R` uses `sapply` instead of the parallel-aware `my.sapply` for the bootstrap p-value computation. This inner loop runs `nboot` (default 100) iterations for each of the ~2,000 L-R pairs — all sequentially.

## Fix
One-line change: `sapply` → `my.sapply` on line 261.

## Results
Tested on 40,000 cells with 64 CPUs:
| Before | After |
|--------|-------|
| ~46 hours | ~5.2 hours |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `623f48f7bb0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.