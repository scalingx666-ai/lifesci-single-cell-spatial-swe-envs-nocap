# Issue

**Title:** Add command-line options to address running out of GPU memory in posterior generation

## Description

Added options --posterior-batch-size and --cells-posterior-reg-calc.

Note that I removed version specifier for cudatoolkit because otherwise there were conflicts with other packages.  I don't know if that was the right thing to do.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `78f005fc8dc9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.