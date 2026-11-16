# Issue

**Title:** Fix pickling for TSNEEmbedding objects; missing optimizer

## Description

##### Issue
Pickling doesn't work for `TSNEEmbedding` objects. 


##### Description of changes
Fix picking. For some reason, things crash if I try to include the `optimizer` in the pickle, even though it's pickled fine on its own. So the optimizer is not included.

In general, this might not be a problem because the typical use case for pickling would be to create the embedding, then use if for subsequent transforms. It can even be optimized later on as well, but the momentum terms will be reset when unpickling.

##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a78c7f08c80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.