# Issue

**Title:** WIP fix path to source code folder in setup.cfg

## Description

This PR addresses the installation issue mentioned in #25. The below now works correctly on Google Collab, for example:

```
!pip install git+https://github.com/nfultz/PaCMAP

from pacmap import pacmap
```

Note that the pacmap module (`pacmap.py`) is within a package also named pacmap (the folder `source_code/pacmap/`), and the package init (the module `source_code/pacmap/__init__.py`) doesn't do anything. 

That is why I had to do `from pacmap import pacmap` which looks weird. 

This PR is on a different branch than #27 so that I can continue to work against my own main branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9fcd45d1da36`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.