# Issue

**Title:** Add knn_kwargs parameter to TSNE API

## Description

##### Issue
<!-- E.g. , Implements #2, etc. -->
<!-- Or a short description, if the issue does not exist. -->
Discussed this with @dkobak earlier today and saw that there is already an issue present. 

This PR  

##### Description of changes

We add `knn_kwargs` as a dict and pass that through to where the knn index is created.  I added some parameters to Annoy (`n_trees`) and Pynndescent (`n_trees`, `n_iter`, `max_candidates`).

##### Includes
- [X] Code changes
- [ ] Tests
- [X] Documentation (docstring)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `80d4f3dc4b8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.