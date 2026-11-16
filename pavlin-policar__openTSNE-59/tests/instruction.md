# Issue

**Title:** Add scikit-learn API

## Description

##### Issue
While the API is fairly similar to scikit-learn, it's still annoying to switch out different methods due to openTSNE returning the embedding from `fit` and scikit-learn returning the fitter object. This means that when I want to switch out MDS for t-SNE, I not only need to change the object but also the method from `fit_transform` to `fit`.


##### Description of changes
Implement scikit-learn API.

##### Includes
- [X] Code changes
- [X] Tests
- [X] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3a9b2c59f24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.