# Issue

**Title:** Use splice position in read key

## Description

get_read_position will now use the position of the FIRST splice junction in the read (in reference coords) in the key if spliced-is-unique is set instead of just true or false.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0164d7c85bbd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.