# Issue

**Title:** MCKP gene iterator speedup

## Description

There is an iterator which gives logical arrays used to index the COO sparse posterior object, for the purposes of breaking it up into "independent" chunks for MCKP estimation.  (This is just achieved by having all entries for a given gene within a single chunk, since each gene is independent of every other during MCKP estimation.)

Previously, it was implemented as a generator which would `yield` a logical array.  The implementation was a bit clumsy.

Now, it is implemented as a simple list, computed as fast as I can figure.  The speedup for large posterior COO objects is at least a factor of 100.  This is very important, since for large datasets it was taking quite a long time in some cases, like on the order of 10 minutes or more, it seemed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8be31d2bc02f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.