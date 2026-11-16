# Issue

**Title:** Support gzipped proteins as input

## Description

Dear CheckM team,

Uncompressing thousands of gzipped faa files just to run them through CheckM can be a bit of a pain. Since many proteins are predicted from a large MAGs collection, it is beneficial to support gzipped proteins as input directly for CheckM.

Best regards,
Jie

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b42a8ca13dd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.