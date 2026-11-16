# Issue

**Title:** {is} remove tryexcept

## Description

Removes try except statements from around the import statements. 

I think these were neccessary because previously if you imported ran in a local directory that contained an `umi_tools` package, it would try to load from there and then get confused, which messed with the tests. This is fixed by adding `from __future__ import absolute_import`
also moved `matplotlib` backend specification to umi_methods.py from `umi_tools.py`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e492779f3eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.