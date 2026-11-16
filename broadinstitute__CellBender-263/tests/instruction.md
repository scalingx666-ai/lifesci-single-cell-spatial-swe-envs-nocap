# Issue

**Title:** Memory-efficient posterior generation

## Description

It has become apparent that something during the posterior generation process in v0.3.0 is gobbling up way too much memory, more than previous versions.   #248 

Conceptually, in v2:
- for each minibatch
    - compute the posterior
    - estimating the noise counts
    - keep only the noise counts

Conceptually, in v3:
- for each minibatch
    - compute the posterior
    - keep a sparse representation in memory
- save the full sparse posterior as an h5 file
- use an "estimator" applied to the full sparse posterior

This refactor allows us to do a whole lot more.  But it also involves computing and saving the full posterior, which was not attempted in v2.  While it is perfectly doable (these posterior h5 files are usually less than 2GB), it seems it needed to be done a bit more carefully.

I think the extension of python lists left around objects in memory (by creating references to them) that I did not intend.

Adopting another strategy: keep a python list of (sparsified info as) torch tensors.  Append tensors to the lists each minibatch.  Concatenate them once and for all at the end.  All these tensors are cloned from the originals, detached, and kept in cpu memory.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da9fabb335f4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.