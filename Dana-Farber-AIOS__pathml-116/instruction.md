# Issue

**Title:** DICOMBackend

## Description

`DICOMBackend` enables full support for DICOM images. Individual frames are read from the DICOM image without loading the entire image into memory. I also made the tests for all the backends more organized.

This code was written mostly by David. I just refactored it to fit in our design.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97cd692d5daf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.