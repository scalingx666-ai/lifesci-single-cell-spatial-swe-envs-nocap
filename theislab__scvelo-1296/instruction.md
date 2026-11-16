# Issue

**Title:** Update _logging.py

## Description

## Bug fixes
The `print_version()` function in `scvelo/logging/_logging.py` incorrectly attempts to import `__version__` using a relative import (`from . import __version__`).  The `__version__` attribute is defined at the top level of the `scvelo` package, not within the `logging` submodule, causing the import to fail.
```python
>>> import scvelo as scv
>>> scv.logging.print_version()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/opt/conda/lib/python3.12/site-packages/scvelo/logging/_logging.py", line 187, in print_version
    from . import __version__
ImportError: cannot import name '__version__' from 'scvelo.logging' (/opt/conda/lib/python3.12/site-packages/scvelo/logging/__init__.py)
>>> print(scv.__version__)
0.3.3
```
Changing to `from scvelo import __version__` solve the issue.
```python
>>> import scvelo as scv
>>> scv.logging.print_version()
Running scvelo 0.3.3 (Python 3.13.2) on 2025-02-24 12:00.
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `22b6e7e6cdb3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.