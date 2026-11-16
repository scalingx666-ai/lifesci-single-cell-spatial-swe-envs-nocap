# Issue

**Title:** Amortised inference for cell2location (hierarchical messenger guide + aggressive training)

## Description

- Hierarchical amortised inference messenger guide.
- Aggressive training plan.
- Mutual information computation between input data and amortised NN output.
- Modified version of FCLayers from scvi-tools with each layer starting rather than ending in dropout (aka applying dropout to NN input data).
- Improved posterior quantile computation and tests.
- Other experimental features.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c455fa6f479`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.