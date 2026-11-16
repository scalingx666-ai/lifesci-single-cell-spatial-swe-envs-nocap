# Issue

**Title:** Add support for Xenium protein data

## Description

- Xenium 4.0 will produce a new feature type called "Protein Expression"
- In order to limit breakage of downstream tools, it stores values as integers multiplied by 10 (essentially fixed point).
- This scaling factor is stored in the HDF5 file as an attribute called `protein_scaling_factor`
- This PR loads the new feature type and applies the scaling factor when it is available.

<!--
Thanks for your interest in contributing! 

Please refer the contributor's guide for instructions on submitting a pull request:
https://github.com/satijalab/seurat/wiki#contributors-guide
-->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ad32ee87219f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.