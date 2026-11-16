# Issue

**Title:** Merge latest version of `release/0.2.4`

## Description

## Changes

* Update CI to run on release branch.
* Update `recover_dynamics` docs.
* Update issue template.
* Add arguments for stream plot to `pl.velocity_embedding_stream`.
* Fix matplotlib warnings (#516)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f4a6c2eb2062`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.