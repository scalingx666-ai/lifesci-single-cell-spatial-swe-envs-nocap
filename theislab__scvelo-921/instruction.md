# Issue

**Title:** Fix bug with clean_obs_names

## Description

Switched implementation to use the previously ignored id_length
parameter. New approach finds a substring of length id_length
where each of the letters are in the alphabet

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32ce21b9484f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.