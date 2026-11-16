# Issue

**Title:** Implement averaging multiscale affinities

## Description

##### Description of changes
- Allow changing perplexity list in multiscale affinities.
- Implement multiscale affinities using averaging technique instead of using the multiscale kernel.


##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `11e43a3dad76`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.