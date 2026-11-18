# Issue

**Title:** Run the tutorial notebooks in CI

## Description

Adds `test_tutorials.yaml`, which executes each tutorial notebook in its own runner and caches the datasets `li.ds` downloads.
Running them locally surfaced three breakages that are fixed here (a pandas >=3 error in `li.ds.kang_2018`, an `np.asarray` around the sparse connectivities in `MistyData`, and the missing graphviz dependency of `targeted.ipynb`); `liana_pyCrossTalkeR.ipynb` and the three MERFISH notebooks are commented out of the matrix with the reason next to each, and the submodule points at scverse/liana-tutorials#3, which has to be merged first.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d80a6d3d1f30`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.