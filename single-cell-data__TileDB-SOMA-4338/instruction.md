# Issue

**Title:** [Backport release-2.2] [python] Use importlib.metadata.version instead of __version__

## Description

Backport dc42c79e79a1a87ed0ca02e821ed93d073de0234 from #4316.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b381ba18a615`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.