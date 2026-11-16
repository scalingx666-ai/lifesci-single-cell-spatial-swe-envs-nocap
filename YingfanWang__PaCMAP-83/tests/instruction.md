# Issue

**Title:** prototype support for `n_components=1`

## Description

```bash
$ uv run --with 'ipython, git+https://github.com/mathematicalmichael/PaCMAP@feature/unit-dimension' ipython
 Updated https://github.com/mathematicalmichael/PaCMAP (42a630b)
Installed 26 packages in 243ms
```
```ipython
Python 3.11.9 (main, Aug 14 2024, 04:17:21) [Clang 18.1.8 ]
Type 'copyright', 'credits' or 'license' for more information
IPython 8.29.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: from pacmap import PaCMAP

In [2]: PaCMAP(n_components=1)
Warning: Defaults were chosen around dimension 2. Dimension 1 has not been tested.
Out[2]: PaCMAP(n_components=1, random_state=0)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dcd0abd1a75a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.