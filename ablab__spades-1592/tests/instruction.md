# Issue

**Title:** Fix standalone tool compilation

## Description

Currently, standalone tool compilation via `spades_compile.sh -a` is broken due to minor bugs in unit tests and MTS. This is resolved by

- Porting `loser_tree_test.cpp` to gtest
- Applying `seq` namespace in `kmer_multiplicity_counter.cpp`

Additionally, compilation flags in the documentation are updated to the correct version.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ab1fbacf255`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.