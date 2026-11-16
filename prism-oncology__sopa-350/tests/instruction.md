# Issue

**Title:** WSI compute_embeddings cleanup

## Description

Hi @stergioc, I made some updates regarding the `compute_embeddings` function:
- better docstrings (some things were outdated, e.g. the type of the output, which is now an Anndata object and not an image)
- I moved the model logic out of the _inference file. The idea is to keep only the loader logic inside this file. I think it was very confusing to have one file called infer and one _inference. This way, after this PR, we can rename this file into _tile_loader or _loader.

What do you think?

NB: the CI is failing because the cellpose server is down, but it should be resolved soon (I hope)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5768b5542b00`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.