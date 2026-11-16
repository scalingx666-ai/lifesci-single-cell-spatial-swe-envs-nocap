# Issue

**Title:** Grst master

## Description

@grst I am not sure if you will be able to see this but I made two changes on top of your submitted PR,

1) I added a trailing slash that was removed from the get_url method
2) I added environment variables to control the behavior of ProxyFix. The behavior that you originally implemented should be achieved by setting the following environment variables:

```
PROXY_FIX_PROTO=1
PROXY_FIX_HOST=1
PROXY_FIX_PREFIX=1
```
And of course I fixed the failing unit tests.
Please confirm and I will merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `942410bb447e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.