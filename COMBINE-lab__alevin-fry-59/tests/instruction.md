# Issue

**Title:** Parsimony USA  mode + other changes

## Description

Add support for `parsimony`, and `parsimony-em` in USA mode.  Added 2 new resolution methods `parsimony-gene`, and `parsimony-gene-em` mode (both work in USA mode or non-USA mode).  Changed default output to `mtx` format and added `--use-eds` flag.  Added (hidden) `--umi-edit-dist` flag for future use. Currently, it can force the parsimony modes to build PUGs only on identical UMIs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41770ae16110`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.