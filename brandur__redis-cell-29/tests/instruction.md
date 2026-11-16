# Issue

**Title:** fix redis command key define

## Description

Fix command key info when create_command.

The command key info is used in redis cluster. Incorrect command key info will cause cluster can not redirect key to the correct node.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd3a6c974a83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.