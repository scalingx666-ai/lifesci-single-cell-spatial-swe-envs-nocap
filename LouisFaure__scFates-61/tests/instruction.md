# Issue

**Title:** Fix slide_cells edge cases in region_extract

## Description

Two edge-case bugs in scf.tl.slide_cells reported in #60:

1. When the first principal point already exceeds the window, inds[0]
   is 0 and the pps_region slice [:0] returns an empty window, producing
   a NaN pt_cur that breaks the recursion. Keep at least that point.

2. In the two-branch case, a branch may run out of cells for the current
   pseudotime, making its pt_cur NaN and crashing the recursive call.
   Only recurse into branches that still have cells to extract.

Claude-Session: https://claude.ai/code/session_0152pVAvAhGXQuWepi4YbWYn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4c9f88b6fd6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.