# Issue

**Title:** Attempted fix to segfault in issue #281 and #279

## Description

Here is the fix for issue #281 and #279, the Rcpp script has been modified to get the indicies of columns instead of assuming them. The testcase for contig_list passes still and my local tests on the input file also work. It would be good to add more tests in the future for other file formats.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7890fdbd8c9f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.