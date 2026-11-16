# Issue

**Title:** Implement binary uniform affinity

## Description

This is a very minor suggestion, but I realized some time ago that in some papers we implement "uniform affinities" slightly differently: not as `(P + P.T) / 2` but as `(P + P.T > 0).astype(float)` where `P` is the kNN adjacency matrix. The only difference is that the former has two possible non-zero values, whereas the latter has only one possible non-zero value, which is kind of neat.

This does not really make much of a different in practice, but I thought it may be nice to implement it in `Uniform()` using `symmetrize="average"` and `symmetrize="or"`, in addition to `symmetrize=True/False` which this class has anyway.

![tsne-uniform-two-kinds](https://github.com/pavlin-policar/openTSNE/assets/8970231/50f0ba1b-3097-4ab9-bbab-dfb3d42ad04f)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a46fae0f4360`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.