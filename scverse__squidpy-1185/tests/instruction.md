# Issue

**Title:** chore: switch to dependency groups

## Description

Switches to dependency groups so the development dependency groups `test`/`dev`/`docs` are no longer “features” that users can see and install when installing squidpy.

Also formatted `hatch.toml` in the way that pyproject-fmt does. I can undo that if you don’t like it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4fb7ebd15029`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.