# Issue

**Title:** Use `np.float64` in kmeans to improve zero_shot reproducibility

## Description

Improves #33, but reproducibility is still not 100% guaranteed (limitation of sklearn...), although the difference of the centroids of different runs is usually lower than 1e-16.

Note also that #60 also helps fix this issue: this will be available in `novae==1.1.0`, and a tutorial about this will be available

Minor: I also filtered a scanpy warning (can't switch to squidpy because squidpy is not in the novae deps).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8717bc1c1227`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.