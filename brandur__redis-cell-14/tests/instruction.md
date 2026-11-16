# Issue

**Title:** Check for emptyness of writable string before parsing

## Description

Fixes 

The rationale for this check is already explained in existing code: https://github.com/brandur/redis-cell/blob/master/src/redis/mod.rs#L299-L304

As I'm not familiar to the code, I decided to modify it at the user side, but maybe a better solution might be to modify `RedisKeyWritable.read()` to return `None` for empty strings. What do you think @brandur?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb530c8fe0e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.