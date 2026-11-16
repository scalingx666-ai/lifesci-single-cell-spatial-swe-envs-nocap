# Issue

**Title:** Overhaul of build system.

## Description

* Custom backend is now gone, and uses setuptools.build_meta.
* specifies pre-cythonized _umi_tools.c as the extension
* references to ez_setup.py removed.
* created github action to build wheels using cibuildwheel
* Will build wheels on tag.
* Will publish to PyPI on published release using trusted publisher model, rather than persistant token.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb79d7bc1b73`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.