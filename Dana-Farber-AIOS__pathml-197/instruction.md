# Issue

**Title:** Release v1.0.2

## Description

This release has changes to environment specifications to make installation process smoother:
-  Removed deepcell from environment.yml, as it was causing environment setup process to hang (#195)
- Pinned all versions in environment.yml to ensure reproducible development and testing environment
- Unpinned versions in setup.py install_requires to make installation more flexible for users, which will hopefully avoid dependency conflicts with other packages (#190)

Also some bugfixes: (#192, #193)
And the addition of the "shape" attribute to the .h5path specification

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `538de4bbbb82`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.