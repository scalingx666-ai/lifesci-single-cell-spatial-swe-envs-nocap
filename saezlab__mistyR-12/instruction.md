# Issue

**Title:** Fixed deprecation of `multiprocess`

## Description

Fixes error on installation:
```
error: Initialization of plan() failed, because the test future used for validation failed. The reason was: (converted from warning) Strategy 'multiprocess' is deprecated in future (>= 1.20.0). Instead, explicitly specify either 'multisession' or 'multicore'. In the current R session, 'multiprocess' equals 'multisession'.
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a95b33c6581`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.