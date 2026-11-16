# Issue

**Title:** Transform layers

## Description

This PR allows for the affine transform associated with the layer(s) to be updated when the coordinate system is changed. It will ignore layers that do not have an `sdata` object associated with them. 

Furthermore, this PR includes a bugfix for the issue of  a `KeyError` being raised when the visibility of the layer is updated and the layer has no `sdata` associated with it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d674bcd0ce49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.