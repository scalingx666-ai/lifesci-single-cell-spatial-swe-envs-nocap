# Issue

**Title:** Add support for AnnData inputs

## Description

Addresses #88 

Hey CellBenders,

This PR adds support for AnnData inputs. Two questions:

1. Do you think throwing a `logger.warning(...)` when few barcodes are present in the AnnData object is sufficient to prevent misuse of `remove-background` on pre-filtered data?
2. I added a test for anndata loading to `remove-background/tests/test.py`, but it looks like both tests were failing in my checkout. I fixed `test_data_simulation_and_write_and_read` but left `test_inference` as is. Are these still WIP and known to be failing?

Happy to adjust anything as you see fit.

Best,
Jacob

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41cf6ec16a3b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.