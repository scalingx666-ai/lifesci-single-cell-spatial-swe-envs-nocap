# Issue

**Title:** Options for using pre-filtered read1s

## Description

This commit adds the `--reconcile-pairs` option to `extract`.

In this mode, as `extract` iterates through the read1 and read2 fastqs, it compares the first part of the read names. If they are not identical, read2 is advanced until a matching read is found.

This is useful if read1s have already been filtered for whitelisted barcodes without considering read2s, thus only read2s for read1s that have not been filtered will be output.

The default behaviour has been changed such that when this mode is not active (default), an error is thrown if the first part of the read1 name does not match the first part of the read2 name.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f383296ea74f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.