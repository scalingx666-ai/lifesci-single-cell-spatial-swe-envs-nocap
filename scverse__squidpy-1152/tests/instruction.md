# Issue

**Title:** cache hed scores in qc_metrics

## Description

No need for file and thread level caching this way. These functions arent used anywhere else so it's better if they stay pure and the caching is done by the callers and not done in a hacky way.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `541d8f4a8898`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.