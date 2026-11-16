# Issue

**Title:** Update deprecated scipy attributes

## Description

scipy deprecated the csr_matrix.A attribute awhile ago and it was fully removed as of v1.14.0 (https://docs.scipy.org/doc/scipy/release/1.14.0-notes.html). 

Here is a PR in another theislab project that does a similar fix 

@Koncopd I'm not sure if I got all of them (I had this issue when trying to use scPoli with a more recent version of scipy).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe7f72b34261`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.