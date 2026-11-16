# Issue

**Title:** cross-compatibility w/ old and new setuptools

## Description

(hi Donovan!)

fixes the warning flagged @ 
```
UserWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html. The pkg_resources package is slated for removal as early as 2025-11-30. Refrain from using this package or pin to Setuptools<81.
```

at least as of setuptools 82, can no longer import pkg_resources so `checkm` falls down with
```
  File "/usr/local/lib/python3.10/site-packages/checkm/checkmData.py", line 25, in <module>
    from pkg_resources import resource_filename
ModuleNotFoundError: No module named 'pkg_resources'
```

alternately, could simplify the solution by requiring setuptools 81+

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c11fed446ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.