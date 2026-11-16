# Issue

**Title:** perf: illico + numba threads

## Description

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [ ] Closes #
- [x] [Tests][] included or not required because: 
<!-- Only check the following box if you did not include release notes -->
- [ ] [Release notes][] not necessary because:

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

@ilan-gold this is a small PR that does a few things:

- illico previously wasn't getting a thread value passed down (e.g. n_jobs), it was defaulting to 1. that is fixed
- there was a preexisting bug with the _numba utility for resolving thread count, it resolved -1 to 1 thread. the only place it was used was in rank_genes_groups, which passed n_jobs, so this conflicted with scanpy docs. This now properly sets to the numba thread count
- we also wrap the illico call with the _numba utility so numba thread count restores upon completion (I think illico modifies numba thread count, this helps prevent side effects).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dde009ad450a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.