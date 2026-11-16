# Issue

**Title:** Address MCKP memory issues

## Description

It has been observed that the MCKP estimator hogs a ton of memory!  In some cases where there is a massive genome, or where we have RNA + ATAC, so a ton of features, we get `MemoryError`s even on a machine with 64GB memory.  This is totally unacceptable.

This introduces a new chunking strategy to perform the MCKP estimation in chunks.  This seems to be no slower than doing the whole thing at once!  So it seems to save memory for free.  It might even be marginally faster, if the chunks are not too small.

Addresses a few minor issues with report and logging as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0336d585a508`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.