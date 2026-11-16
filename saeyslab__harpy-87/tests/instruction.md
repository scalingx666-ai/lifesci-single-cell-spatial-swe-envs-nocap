# Issue

**Title:** Remove setup.cfg

## Description

pyproject.toml can support everything setup.cfg can. It's also more future proof.

Instead of locking dependencies in a requirements.txt (which does not support optional dependencies), there is now support for `uv lock` and `pixi`.

By using optional-dependencies instead of the newer but not yet supported by pip dependency-groups, nothing changes.

The build backend remains the same, so everything should still work...

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `20e5ac9327f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.