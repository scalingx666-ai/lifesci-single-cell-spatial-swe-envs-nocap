# Issue

**Title:** fix(sandbox): resolve the runtime venv by path, so the pantheon CLI runs

## Description

`pantheon --help` in a sandbox terminal died on:

```
ModuleNotFoundError: No module named 'fire'
```

with `fire` sitting in `/venv/lib/python3.12/site-packages` all along.

`PANTHEON_RUNTIME_PYTHON` was resolving to `/usr/local/bin/python` — the base image's interpreter, which has none of the agent's packages. It asked `command -v python`, and PATH is not reliable here: `/etc/profile` rebuilds it for a login shell and drops the `/venv/bin` that Docker's `ENV` put there.

It now looks at `VIRTUAL_ENV` and `/venv` directly and asks PATH last.

The second half of the bug was the guard. This file is sourced repeatedly, the first sourcing had already recorded the wrong answer, and `if [ -z ]` only fills in a blank — so the wrong value would have survived every later correction. A value that cannot import the agent's own dependencies is now replaced rather than kept.

Verified in a sandbox: `PANTHEON_RUNTIME_PYTHON=/venv/bin/python`, and `pantheon --help` reaches its own output.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10435665c334`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.