# Issue

**Title:** Change gradient descent to object to keep gains through runs

## Description

##### Issue
Calls to `optimize` didn't save state and had to start with empty gains, potentially slowing down convergence. This may be problematic for larger data sets.

See  for discussion.


##### Description of changes
Change `gradient_descent` into an object that stores gains.


##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb2145167b5f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.