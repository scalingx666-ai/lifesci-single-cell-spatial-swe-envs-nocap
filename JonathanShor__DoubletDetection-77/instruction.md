# Issue

**Title:** Removed requirement that cluster IDs be bumped up if -1 cluster

## Description

- Cluster IDs reflect Phenograph outputs; -1 always represents cells that are not clustered.

- Community IDs should only reflect communities with original cells in them.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4207cc2436d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.