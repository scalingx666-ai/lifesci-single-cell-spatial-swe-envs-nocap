# Issue

**Title:** break up _metrics into separate functions

## Description

When _metrics fails, it is impossible to debug due to many computations being squashed into on NJIT function. This separates each metric into its own function, using NJIT when appropriate. See https://github.com/openproblems-bio/openproblems/actions/runs/3388609861/jobs/5633837315#step:19:2770

Passing benchmark at https://github.com/scottgigante-immunai/openproblems/actions/runs/3394490431

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `372405119007`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.