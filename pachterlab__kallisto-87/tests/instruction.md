# Issue

**Title:** Bias to hdf5

## Description

This PR creates 3 new fields in the HDF5 output.
- fld the fragment length distribution counts
- bias_observed the observed counts for each 6-mer
- bias_normalized the counts of 6-mers normalizes with respect to the abundances of transcripts

In case the fld was not estimated from the data, an all zeros vector is written

In case the bias was not estimated from the data an all ones vector is written for both the bias vectors.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `36a8d854389f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.