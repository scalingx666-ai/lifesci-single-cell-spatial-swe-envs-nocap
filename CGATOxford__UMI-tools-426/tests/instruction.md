# Issue

**Title:** Resolves travis fails

## Description

After a bit of digging, the source of the travis fails has been identified as `samtools` v1.10 (https://github.com/samtools/samtools/releases/tag/1.10) which now adds a header line to the output sam, containing the sort command itself. I took the easy route out and added the `--no-PG` to our `samtools sort` call. If we think that users may actually want to have this line included in the header for downstream purposes, we can update test script to strip the line out (since it includes the output directory which is randomly generated at test run time).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f380afe7803`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.