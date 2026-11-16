# Issue

**Title:** [c++] Update default log level to warn

## Description

**Issue and/or context:** [SOMA-844]

**Changes:** Changes the default logging level in `libtiledbsoma` from `INFO` to `WARN` to reduce noise for users and in the R package's test outputs. The `INFO` log level outputs implementation details that are useful for debugging but not actionable for typical users, e.g.:

```log
[2026-01-26 14:09:47.651] [tiledbsoma] [Process: 93743] [Thread: 38614402] [info] [JoinIDCache] Loading obs joinids
[2026-01-26 14:09:47.739] [tiledbsoma] [Process: 93743] [Thread: 38614402] [info] [JoinIDCache] Loading var joinids
[2026-01-26 14:09:48.422] [tiledbsoma] [Process: 93743] [Thread: 38614402] [info] Adding assay 'RNA'
```

**Notes for Reviewer:** Python's `tiledbsoma.logging` module already defaults to `WARNING`. Changing the C++ default to `WARN` aligns both language APIs to the same default level.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cefbd3afdfdf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.