# Issue

**Title:** Add gamma parameter for smoothing affinity rows in PerplexityBasedNN

## Description

This adds an optional gamma parameter to PerplexityBasedNN and joint_probabilities_nn. Each row of the conditional probabilities is raised to the power gamma and renormalized before symmetrization. gamma=1 (default) gives standard t-SNE, gamma < 1 smooths each row, and gamma > 1 sharpens it.

gamma is also used by set_perplexity and to_new. I added 8 tests (including a check that the transform equals rescaling the Gaussian bandwidth by 1/√gamma) and a short entry in the parameter guide as you suggested.

Paper: https://arxiv.org/abs/2608.17190

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d7f5cf621e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.