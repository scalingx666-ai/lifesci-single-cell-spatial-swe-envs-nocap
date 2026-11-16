# Issue

**Title:** fix(space): correct SpaceFlow and STAGATE training and spatial inputs

## Description

Correct result-changing defects in SpaceFlow and STAGATE training and spatial inputs.

SpaceFlow now uses matching independent cell pairs for latent and spatial distances, handles zero distances without non-finite normalization, and retains an independent copy of the best training weights. Pseudospatial roots are mapped from sampled positions back to the original observation indices in both model wrappers and vendored SpaceFlow.

STAGATE builds its tiled and full graphs from the selected coordinates without overwriting the caller's spatial coordinates. It rejects zero training epochs and prediction before training. Ordinary Tensor edge indices no longer require the compiled torch-sparse extension.

The change is limited to four implementation files and one regression test file. These corrections can change previously affected embeddings and pseudospatial results; affected analyses should be recomputed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41531a627523`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.