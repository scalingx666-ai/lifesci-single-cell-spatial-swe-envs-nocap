# Issue

**Title:** Bypass spatial join when using only one patch to speed-up `make_transcript_patches`

## Description

- When running `make_transcript_patches` with only one patch and no tissue segmentation, it's not needed to run the spatial join to check which transcripts are in the patch. It will speed-up the operation, and also reduce the RAM usage.
- Minor syntax change to iterate over partitions. It will make it easier to change the scheduler config if needed in the future
- Added a small test

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10ee6f963f05`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.