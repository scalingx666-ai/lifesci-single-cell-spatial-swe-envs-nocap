# Issue

**Title:** Add proper conda/pip include dirs to C compilers

## Description

##### Issue
Wasn't finding FFTW3 headers even if they were available in the conda environment.

##### Description of changes
Add proper include directories to C compilers.

Also, the installation will now raise an Error if the Python version is too low. Hopefully, this will avoid future confusion about what should and should not work.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73e77e0b664a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.