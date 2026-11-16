# Issue

**Title:** Allow decreasing perpleixties in perplexity based affinities

## Description

##### Issue
Following the art of using t-SNE, good results can be obtained by first running t-SNE at a high perplexity to capture global structure, then decreasing to account for more local structure.

##### Description of changes
Add `set_perplexity` method to `PerplexityBasedNN`. This allows lowering the perplexity without having to first recompute all the nearest neighbors. Proper bandwidths for the Gaussians still need to be recomputed in order to form a new affinity matrix.

##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b9fb43d7a24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.