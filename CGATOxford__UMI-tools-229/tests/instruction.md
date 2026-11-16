# Issue

**Title:** Alter iter_nearest_neighbours to produce combinations not permutations

## Description

I realised that currently the `iter_nearest_neighbours` function, which is used for umi bundles > 25, produces pairs similar to those produced by `it.permutations`, i.e. (B, A) as well as (A, B), whereas for umi_bundles < 25, `it.combinations` is used (producing just (A, B)). This change would make the `iter_nearest_neighbours` function also produce combinations. I don't know whether this bug had any difference on the output, but even if not I think it should reduce the number of pairwise edit distances that have to be computed even further (by exactly half, I'm guessing...?)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73d4169fe521`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.