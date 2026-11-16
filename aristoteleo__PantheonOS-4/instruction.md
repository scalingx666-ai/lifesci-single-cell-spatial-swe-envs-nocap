# Issue

**Title:** fix log error

## Description

Changes:

1. Remove the logger hander setting in `Repl.run` to avoid replace the main setting in core.py
2. Set log level to 'INFO' as default in core.py

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a2f2c24bb9ea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.