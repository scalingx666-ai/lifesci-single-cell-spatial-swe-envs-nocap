# Issue

**Title:** Demonstration of the optgroup concept.

## Description

Not to be merged, as we want to do a few things:

- Show QC metrics in the "Computed" category.
- Divorce the supplied and computed covariates in the `annotationCols`, to eliminate potential for confusion.

![Screenshot from 2022-11-02 22-52-05](https://user-images.githubusercontent.com/8166669/199655508-2a04e794-a299-4293-9358-82dddd428980.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b0156090f48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.