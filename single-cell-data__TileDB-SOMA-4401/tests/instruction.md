# Issue

**Title:** Clean-up soma_array header

## Description

Issues: Closes SOMA-853

Changes:
* Forward-declare many of the classes/structs used by the SOMAArray class
* Remove or inline unused/rarely-used functions

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed7836c7dfe3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.