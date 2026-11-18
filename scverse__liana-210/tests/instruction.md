# Issue

**Title:** support for python 3.13

## Description

this addresses #188 

I added a test environment for python 3.13, and pinned `gseapy>=1.1.0` to the `optional-dependencies.extras`. Without this gsea dep, uv failed to install gseapy for python 3.13, which is needed by cell2cell.

The tests still fail, but they fail with the same errors as python 3.12 fails atm.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b9b5619c642`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.