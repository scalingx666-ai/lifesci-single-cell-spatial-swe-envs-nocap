# Issue

**Title:** Fix/dynamics classes

## Description

## Changes

* Makes arguments `adata` and `gene` required arguments for instantiating `BaseDynamics` and `DynamicsRecovery`
* Simplifies the inheritance from `BaseDynamics` in `DynamicsRecovery`

## Related issues

. . .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b00a96419e4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.