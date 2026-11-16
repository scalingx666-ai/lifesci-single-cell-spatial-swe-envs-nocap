# Issue

**Title:** Add tcrblosum support to TCRdist

## Description

So far, the TCRdist metric used a distance matrix derived from the blosum62 substitution matrix. This PR extends TCRdistDistanceCalculator with a new base_matrix="tcrblosum" option alongside the existing default blosum62 behavior. This way, distance matrices based on the tcrblosum substitution matrices (different matrices for alpha and beta chain) are used for the TCRdist metric calculation.

I try to illustrate how I derived the tcrblosum based distance matrices in this [google colab notebook](https://colab.research.google.com/drive/1K5UFs6bWWBJkN7l3BndkhJ2wGKKtHzZV?usp=sharing).

The usage of the tcrblosum matrices was already discussed in #591.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38f05cdaac83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.