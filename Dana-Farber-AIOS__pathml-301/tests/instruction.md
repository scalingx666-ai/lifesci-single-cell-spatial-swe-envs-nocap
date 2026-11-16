# Issue

**Title:** Update quantify mif

## Description

A couple minor updates to QuantifyMIF:

* update the functional implementation `F()` to not require a tile object. Instead it can be applied on any given image and mask
* Add "label" property to counts matrix. This is useful for linking the counts matrix to the image and mask

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65ecf6c47fd3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.