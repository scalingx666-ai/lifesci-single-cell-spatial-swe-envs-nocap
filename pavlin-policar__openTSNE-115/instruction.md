# Issue

**Title:** Add spectral initialization using diffusion maps

## Description

##### Description of changes
.

I ended up implementing diffusion maps only because computationally, computing the leading eigenvectors is much faster than the smallest eigenvectors, and of the various spectral methods, diffusion maps are the only ones that require this. I checked what UMAP does - it uses the symmetric normalized laplacian for initialization - but they manually set the number of lanczos iteration limit, which I don't understand. This seemed like the better option.

@dkobak Do you want to take a look at this? I implemented this using `scipy.sparse.linalg.svds` because it turns out to be faster than `scipy.sparse.linalg.eigsh` and it seemed to produce strange results when I increased the error tolerance, while `svds` results seemed reasonable.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `335f048100f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.