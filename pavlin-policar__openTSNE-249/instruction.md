# Issue

**Title:** setup.py maintenance

## Description

##### Issue
It seems that in the latest version of `pip`, we can no longer pass in a class into `include_dirs` that eventually resolves into a string. This was previously done because running `setup.py` in a fresh environment would fail as numpy had not yet been installed. Therefore, we used a utility `get_numpy_include` class which would import numpy only when it was called, after numpy was already installed. This is apparently no longer supported.

Related issue: #248
Failing tests in PR #246

##### Description of changes
This is most likely no longer needed because we now build using `pyproject.toml`, where we can pre-specify the build requirements, which will always be installed before the `setup.py` script is run. Therefore, we no longer need any checks if numpy is installed.
Similarly, the `have_cython` check is no longer needed in `setup.py` either, as we specify cython as a build dependency in `pyproject.toml`.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `994cf0be15f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.