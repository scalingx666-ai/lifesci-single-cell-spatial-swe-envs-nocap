# Issue

**Title:** Fix major bug in v0.3.1: negative counts

## Description

Something about the update from v0.3.0 to v0.3.1 induced a bug (I'm not yet sure of the scope, but potentially affecting all datasets) where negative counts could be produced in the output.  It is assumed that these outputs are totally compromised.  v0.3.1 has already been redacted, but the master branch is still compromised.

I think the bug probably lies in the updated posterior generation code, which was the target of memory-saving updates in v0.3.1.

Expand tests covering that code.

- unit tests for posterior generation
- integration tests ensuring no negative count matrix entries in the output (not explicitly tested currently)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4da38a2b977`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.