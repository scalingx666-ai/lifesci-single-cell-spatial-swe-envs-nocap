# Issue

**Title:** [r] Fix type confusion in `pseudobulk_matrix()` and clean up `parallel_split()`

## Description

As reported in #173, `pseudobulk_matrix()` assumes that all input matrices are type "double", which results in type confusion in some circumstances. While fixing this, I also noticed an issue in `pseudobulk_matrix`'s use of `parallel_split`, which would needlessly split up a matrix even if no parallelism was requested (slight potential performance/memory hit). I did a small refactor to make `parallel_split` easier to use correctly and resolve the issue in `pseudobulk_matrix`

Changes in this PR:
- Always cast inputs to `pseudobulk_matrix()` to type `double`
- Adjust `parallel_split` logic to not do any splitting if `threads <= 1`
- Adjust other usages of `parallel_split` to take advantage of not needing the conditional logic anymore

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb543d3d8798`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.