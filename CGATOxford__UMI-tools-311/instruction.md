# Issue

**Title:** {ts} barcode extract either read

## Description

Note, the commits on Jan 24 are from a merge with branch `{TS}-EnablePerCellCountTab` (PR #308). Probably best to merge that PR before reviewing the changes herein.

 for motivation
- Implements barcode extraction from read1 *or* read2 with `--either-read`. 
- Implements option to either discard reads where both match, or keep the UMI with highest sequence quality
- Adds test for `--either-read`

I don't have a good input sample for the test so the current input is hacked together from the indrop data (see `tests/README`). Basically swapped read1 and read2 at random and use option to identify which read matches the regex. Of course, the output from this is now garbage. I'll post on #175 and ask for more suitable toy data. Also need to add a test to cover `--either-read-resolve=quality`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f5c0c25fd90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.