# Issue

**Title:** Add support for callable metrics

## Description

##### Issue
<!-- E.g. , Implements #2, etc. -->
<!-- Or a short description, if the issue does not exist. -->
  

##### Description of changes
Added the option for callable metrics to the `openTSNE.nearest_neighbors` module. `NNDescent` checks if metric is compiled with `numba`, gives an informative warning, and then attempts to automatically compile it. If the function is already compiled or `NNDescent` is not being used then the callable is passed without any further checks. Docstrings have also been updated to match other docstrings with multiple types. If you'd like unit tests for this, then please provide guidance on how best to do this. 

##### Includes
- [X] Code changes
- [ ] Tests
- [X] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `23bec00b8f10`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.