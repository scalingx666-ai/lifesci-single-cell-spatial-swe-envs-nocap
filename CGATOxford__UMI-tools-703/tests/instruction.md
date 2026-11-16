# Issue

**Title:** Fix passing of format strings to htslib via pysam.

## Description

pysam needs format strings to be passed as lists of bytes, rather than comma separated strings.

Should fix outstanding issue on #694

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29dc0c6dc900`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.