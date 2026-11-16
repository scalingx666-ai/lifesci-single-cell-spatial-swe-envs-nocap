# Issue

**Title:** Support precomputed distance matrices

## Description

##### Description of changes
.

- Change API for `KNNIndex.__init__` and `KNNIndex.build` so that `data` and `k` are specified in the constructor. This makes more sense in light of the precomputed distance class. This is against what I usually say, that the API needs to be backwards compatible, but I strongly suspect this is so deep within the library that nobody has ever done anything with it. So I think it should be okay here.
- Change API for `TSNE.__init__` and `TSNE.fit`, removing the `affinities` parameter from the constructor. This lead to some very strange function calls. We now change `.fit` so that either a data matrix can be passed in, or an affinity object. Optionally, the user can specify the initialization as well. Same goes for `prepare_partial`. Again, this is such niche usage, I doubt anyone will have problems with this.
- Adds support for precomputed distance matrices

##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa7c5314e031`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.