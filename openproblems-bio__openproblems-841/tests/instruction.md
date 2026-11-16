# Issue

**Title:** Precompute nn ranking for DR datasets

## Description

Adding a bigger dataset to the dimensionality reduction task accidentally cost us $1000, because we're computing pairwise distances on each dataset n_methods * n_nn_ranking_metrics times (which is a lot). This PR is a hack -- we precompute the NN ranking matrix, which is costly upfront, but it only happens once. Ideally we could define bespoke metric dependencies, but that sounds like a v2 feature.

cc @rcannood

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `86375dd2be7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.