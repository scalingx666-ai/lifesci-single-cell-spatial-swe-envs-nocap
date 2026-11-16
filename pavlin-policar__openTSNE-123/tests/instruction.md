# Issue

**Title:** transform: evaluate interpolation grid once

## Description

##### Description of changes
When calling transform, the previous implementation took the most straightforward approach and just recomputed everything on the reference as well as the new points. This is redundant since the reference embedding never changes.

Now, the reference embedding is padded equally on each side and the interpolation grid is computed once. Padding enables points that are not similar to the embedding to move away from the embedding. When new points are introduced, we can then quickly calculate their negative gradient from the precomputed interpolation grid. To prevent points from moving outside the interpolation grid, we enforce a circular boundary on the embedding. This massively speeds up the runtime of transform.

This only changes the FFT implementation. The same could be done for BH, but since that's rarely used, and when it's used it's already really fast, the speedup would be marginal. Maybe some day in the future.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28d767c50f8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.