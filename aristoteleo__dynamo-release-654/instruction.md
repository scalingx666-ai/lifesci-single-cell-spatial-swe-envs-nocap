# Issue

**Title:** Refactor `scatters()` and `scatters_interactive()`

## Description

Optimize the structure of scatter plot functions. In the updated version, all parameters (e.g. cur_basis, cur_layer, cur_color ...) will be prepared before the actual plotting function. Next, the figure will plot axes one by one based on one set of parameters. This modularized structure provides better flexibility

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a053564771b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.