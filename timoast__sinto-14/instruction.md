# Issue

**Title:** Use SAM/BAM opening idiom recommended by pysam

## Description

pysam can figure out whether an input file is SAM, BAM, or CRAM, and open it accordingly (https://pysam.readthedocs.io/en/latest/api.html#pysam.AlignmentFile). Although using `mode="r"` works just fine according to my test, the idiom recommended by the `pysam` documentation is to simply not provide a file mode when opening files, and the `AlignmentFile` object will figure out the type by itself. This PR makes that adjustment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b292e54e7307`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.