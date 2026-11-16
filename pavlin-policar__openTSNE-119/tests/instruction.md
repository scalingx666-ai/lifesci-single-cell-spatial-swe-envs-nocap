# Issue

**Title:** Fixes

## Description

##### Description of changes
- Change verbose learning rate to print 2 decimals.
- Add benchmarks for exact search vs annoy (1000 seems to be an okay cutoff point on 1 core, so leave "auto" parameter as is
- Fix annoy query. Was failing on example notebooks
- Make `pynndescent` an optional, annoy seems faster and enables us to eliminate numba as a hard dependency, making life so much easier.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af3fec4deff0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.