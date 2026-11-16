# Issue

**Title:** Replicate `CL.THROTTLE` invocations to replicas/AOF

## Description

Here we add an invocation to `RedisModule_ReplicateVerbatim` so that
invoking `CL.THROTTLE` will replicate out to replicas/AOF.

This _also_ has the side effect of incrementing a dirty counter within
the Redis server so that RDB snapshots work properly, thus fixing #52.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc05a035183a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.