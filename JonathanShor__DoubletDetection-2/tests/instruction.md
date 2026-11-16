# Issue

**Title:** Supervised classification on synth data

## Description

def syntheticTesting - NBB classifiers on 1D metrics for full dataset.
Runs phenograph to find communities of cells, then NBB & GMM 1D metrics
for each community, GMM on full gene featureset for each community.

GMM is VERY slow, so that needs work.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d758f01c6b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.