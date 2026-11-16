# Issue

**Title:** {ts} include single chrom test

## Description

Does what is says on the tin.
This also hardcodes the pandas version for travis testing to 0.19 since there were issues installing the latest version (0.20 at the time), perhaps relating to the comments ? This hardcoding should be removed when the latest version of pandas can be installed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd652b425ee1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.