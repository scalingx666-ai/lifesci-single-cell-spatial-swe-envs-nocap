# Issue

**Title:** Fix deploy by using local directory

## Description

The `pypa/gh-action-pypi-publish@release` action is a docker-based action and is mounting only part of directories of parent machines. Especially, do not mount `/tmp/` directory where `hynek/build-and-inspect-python-package` is storing the output of build. 

This PR copy output of `hynek/build-and-inspect-python-package` to local directory `dist` to use it in next steeps.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c4d7de7cd46`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.