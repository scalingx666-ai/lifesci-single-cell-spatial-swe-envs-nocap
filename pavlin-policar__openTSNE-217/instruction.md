# Issue

**Title:** Implement precomputed affinity class

## Description

Implements #216.

Allows to do the following:
```python
from openTSNE import TSNE
from openTSNE.affinity import PrecomputedAffinities

# Here P is either a np.array or a scipy.sparse matrix
Z = TSNE().fit(affinities = PrecomputedAffinities(P))
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f79f37ce6752`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.